# Important Links
- [GrafAna Monitoring of the Cold Box](http://eplvm003.ph.bham.ac.uk:3000/d/buq47AcVk/uk_china_coldjig_dashboard_flux)
- [GrafAna Monitoring of the Modules](http://eplvm003.ph.bham.ac.uk:3000/d/JKm4gvAVk/amac_dashboard_flux)
- [Cold Box GUI](http://localhost:5000) <- see instructions
- [Warwick Cold Box Manual](https://espace.cern.ch/ITkColdBox/Shared%20Documents/Coldjig%20assembly%20and%20operation.pdf)
- [Cold Testing Specification](https://edms.cern.ch/document/2228451/3.6)
- [Module Testing Twiki](https://twiki.cern.ch/twiki/bin/view/Atlas/ABCStarHybridModuleTestsV2)

# Our Setup
- Testing is done via the `epldt116` machine using `itkuser2`.
- WebGUI runs on the Raspberry Pi `eplpl004` using `pi`.
- GrafAna and InfluxDB are setups on `eplvm003`.

## Training Modules
There are two prototype modules, `BHM_SS04` and `BHM_LS02`, that can be used to training. There are prototype modules using the v0 chipset and cannot be operated at the same time as production modules. Their config is saved under `training` ITSDAQ setup.

# Checklist for Opening the Box
Opening the lid will bring the lab air (~50% RH) into the box, with a rough dew point of 10°C. If the box is cold, this can cause condensation on the modules or walls. Make sure that the box is warm before opening it.

The power supplies should also be off when disconnecting modules. **Always ramp down HV!** Don't just turn it off.

1. Chiller is at 20°C.
2. Peltiers are set in IDLE mode.
3. Low and High Voltage power supplies are turned off.

# Running A Cold Noise Thermal Cycle
The test runs *X* thermal cycles, with a test at each point. Each thermal cycle
takes 1.5 hours. See specific sections on how to execute specific commands.

1. Make sure that the box is safe to open (see checklist). Especially that the chiller is at 20°C.
2. Make sure that the HV and LV power supply outputs are off.
3. Open the box.
4. Remove caps from the mini-DP connectors.
5. Place modules (testframe and spacer, but without the acrylic covers) on chucks.
6. Fix the modules using four longer screws in the four corners. See Fig 21 in the Cold Testing Specification document.
7. Ground the modules using one shorter screw in the top right corner.
8. Connect the 2x3 molex power cable to the modules. The connector is keyed.
9. Connect the miniDP connectors. The red tagged cable goes to the left (DATA).
10. Close the Cold Box. Check that the GrafAna page says that the box is closed.
11. Turn on dry air (gauge attached on the left side of the box). A good target is 10 L/min.
12. Set the LV power supply output to 11V and current compliance to 5A.
13. Turn on the LV power supply to check a reasonable current draw. The current should read 50 mA * number of modules.
14. Turn off the LV power supply. The coldjig software takes care of powering from now on.
15. Regenerate the configuration with the connected modules.
16. Start ITSDCS with the new configuration.
17. Start ITSDAQ with the new configuration.
18. Set the number of thermal cycles corresponding in the WebGUI to the available time.
19. Select loaded chucks in the left hand side of the WebGUI. Do not fill the module serial numbers (they are ignored).
20. Start the thermal cycling.
21. Wait for thermal cycling to complete. Monitor the GrafAna for issues.
22. Remove modules. Make sure to follow the checklist.

# Starting Testing Software

The testing software consists of three parts:

- The Cold Box GUI accessible via browser at [http://eplpl004:5000](http://eplpl004:5000) on the testing computer.
- The ITSDAQ controller that receives commands from the GUI to run tests.
- The ITSDAQ controller (ITSDCS) that receives commands to monitor Powerboards and control power supplies.

## Cold Box GUI

The Cold Box GUI should always be running to monitor the conditions of the box at all times. The data can be viewed on [GrafAna](http://eplvm003.ph.bham.ac.uk:3000/d/buq47AcVk/uk_china_coldjig_dashboard_flux?orgId=1&from=now-15m&to=now&refresh=5s). If the GUI is not running (ie: [http://eplpl004:5000](http://eplpl004:5000) is not accessible) or needs to be restarted, it can be started by running the following on the `eplpl004` machine. One needs to hop through `eprexb` to access it.

```shell
ssh yourusername@eprexb
ssh pi@eplpl004
cd ~/ppb2_20231004/UK_China_Barrel
pipenv run coldbox_controller_webgui.py -c configs/birmingham_config.ini -v
```

Then navigate to the GUI and click the green "Start" button. In about 10-20 seconds, data should start appearing in GrafAna.

### Shutting Down The GUI
Opening the cold box, even when warm, will trigger the box open warning and spam
the GUI. The only practical way to get rid of them is to restart the GUI.

- Use the red "Shutdown" button. This will stop the thread and the GUI.
- `kill $(ps ax | grep coldbox_controller_webgui.py | awk "{print $1}")` on the `eplpl004` command line.

Doing `Ctrl+C` to the process will not stop it due to a bug in thread management.

## ITSDAQ Control
There are two ITSDAQ macros that need to be running on `epldt116` to control the
modules.

- DAQ: control the module and runs tests
- DCS: monitors the powerboards and controls the power supplies

### ITSDCS Control
The ITSDCS control can be running 24/7. There is no need to restart it for newly
loaded modules.

```shell
cd ~/itk-module-testing-workspace/itsdaq-sw
source ../setup.sh
./INFLUX_AMAC.sh
```

To shutdown ITSDCS control, use `Ctrl+C`.

### ITSDAQ Control
The ITSDAQ control needs to be restarted anytime new modules are loaded. This is
to reload the configuration. See the ITSDAQ configuration for instructions on
how to generate new configurations.

```shell
cd ~/itk-module-testing-workspace/itsdaq-sw
source ../setup.sh
./INFLUX_DAQ.sh
```

To shutdown ITSDCS control, use `Ctrl+C`.

### ITSDAQ Configuration
The ITSDAQ configurations are stored inside `${SCTDAQ_VAR}/config`, where the
`SCTDAQ_VAR` is set by the setup script. There is a `p_d_s` script that can
generate the necessary configuration files.

```shell
cd ~/itk-module-testing-workspace/production_database_scripts
source ../setup.sh
python get_token.py
# copy paste the export command
python strips/modules/getDAQConfig.py --speed640 --encode --id serial --fmc fmcdp --outDir ${SCTDAQ_VAR}/config 2 SERIAL0 4 SERIAL1
```
Replace the `2`/`3` with the position (counting starts at 1 from the left) of
the module with the serial number `SERIAL0`/`SERIAL1`.

# Manually Turning Off a Module
The following commands should be run from the `epldt116` machine if you manually
need to turn off a module.

**Manually confirm that a command has "Completed" by checking for a response in the WebGUI.**. This program only sends the command and does not wait for ITSDAQ response.

```shell
./bin/influx_command --sender COLDJIG --receiver ITSDCS --setup BIRMINGHAM --command HV_OFF
./bin/influx_command --sender COLDJIG --receiver ITSDCS --setup BIRMINGHAM --command HYBRID_OFF
```

Then you can turn off the LV power supply via `LOCAL`, `OUTPUT` on the left
channel.

# Handling Problems
The following lists possible issues that can appear when monitoring GrafAna and
recommended actions to take.

## No Data in GrafAna
Data will stop appearing if the GUI crashed for some reason. The actions are to
restart the whole process.

1. Make sure the HV and LV power supplies are off. See "Manually Turning Off a Module."
2. Restart the GUI.
3. Start test again.

## Dew Point Breached.
If any of the measured temperatures fall below the dew point, it is important to
warm up the box as fast as possible. The HV should be turned off. The LV should
stay on and the hybrids should remain powered.

1. Use the advanced tab to set the chiller temperature to 20C.
2. Stop thermal cycling by killing the GUI process.
3. Start the GUI and only start monitoring. Ensure that the chiller is still set to 20C.
4. Ramp down HV using the following command. Do not turn off hybrids as they help to keep the module warm.
```shell
./bin/influx_command --sender COLDJIG --receiver ITSDCS --setup BIRMINGHAM --command HV_OFF
```

## Missed Command in Influx
Occasionally ITSDAQ misses a command that was sent to it. If a command appears to be taking too long to complete
(no "Compelted" response seen in GrafAna), then check if the responsible commander is actually doing something. If
it is waiting for a command, then you might need to resend it. In a new terminal, source the setup script and run
the following command. Do not close any existing ITSDAQ instances. Make sure to change `ITSDCS` and `HV_OFF` to the
receiver and command that was missed.

```shell
./bin/influx_command --sender COLDJIG --receiver ITSDAQ --setup BIRMINGHAM --command HV_OFF
```
