# Important Links
- [GrafAna Monitoring of the Cold Box](http://eplvm003.ph.bham.ac.uk:3000/d/buq47AcVk/uk_china_coldjig_dashboard_flux?orgId=1&from=now-15m&to=now&refresh=5s)
- [Cold Box GUI](http://localhost:5000) <- see instructions
- [Warwick Cold Box Manual](https://espace.cern.ch/ITkColdBox/Shared%20Documents/Coldjig%20assembly%20and%20operation.pdf)
- [Cold Testing Specification](https://edms.cern.ch/document/2228451/3.6)
- [Module Testing Twiki](https://twiki.cern.ch/twiki/bin/view/Atlas/ABCStarHybridModuleTestsV2)

# Our Setup
- Testing is done via the `epldt116` machine using `itkuser2`.
- GUI runs on the Raspberry Pi `eplpl004` using `pi`. However it is only accessible via `eprexb`. See instuctions for making a tunnel.
- GrafAna and InfluxDB are setups on `eplvm003`.

## Training Modules
There are two prototype modules, `BHM_SS04` and `BHM_LS02`, that can be used to training. There are prototype modules using the v0 chipset and cannot be operated at the same time as production modules. Their config is saved under `training` ITSDAQ setup.

# Checklist for Opening the Box
Opening the lid will bring the lab air (~50% RH) into the box, with a rough dew point of 10C. If the box is cold, this can cause condensation on the modules or walls. Make sure that the box is warm before opening it.

The power supplies should also be off when disconnecting modules. **Always ramp down HV!** Don't just turn it off.

- [ ] Chiller is set to 20C or turned off.
- [ ] Peltiers are set in IDLE mode.
- [ ] Low and High Voltage power supplies are turned off.

# Starting Testing Software

The testing software consists of three parts:

- The Cold Box GUI accessible via browser at [http://localhost:5000](http://localhost:5000) on the testing computer.
- The ITSDAQ controller that receives commands from the GUI to run tests.
- The ITSDAQ controller (ITSDCS) that receives commands to monitor Powerboards and control power supplies.

## Cold Box GUI
The Cold Box GUI should always be running to monitor the conditions of the box at all times. The data can be viewed on [GrafAna](http://eplvm003.ph.bham.ac.uk:3000/d/buq47AcVk/uk_china_coldjig_dashboard_flux?orgId=1&from=now-15m&to=now&refresh=5s). The GUI is accessible only from the test building network at [http://epldt033.ph.bham.ac.uk:3000](http://epldt033.ph.bham.ac.uk:5000).

If and only if the GUI is not running (ie: [http://localhost:5000](http://localhost:5000) is not accessible), it can be started by running the following on the `eplpl004` machine (`ssh pi@eplpl004` from the testing computer).

```shell
cd ~kkrizka/run
source ../venv/bin/activate
coldbox_controller_webgui.py -c configs/config.ini
```

Then navigate to the GUI and click the green "Start" button. In about 10-20 seconds, data should start appearing in GrafAna.

### Shutting Down The GUI
The GUI should be running 24/7 and not turned off. However in case you need to stop it, there are two options:

- Use the red "Shutdown" button. This will stop the thread and the GUI.
- `kill $(ps ax | grep coldbox_controller_webgui.py | awk "{print $1}")` on the `eplpl004` command line.

Doing `Ctrl+C` to the process will not stop it due to a bug in thread management.

## ITSDAQ Control
The ITSDAQ is controlled using a special macro that queries the InfluxDB for commands. This should be restarted at the beginning of each thermal cycle. It ensures that each thermal cycle has its down run number in the data file. Also the ITSDAQ config needs to be manually editted for each module configuration.

The ITSDAQ control can be started on the testing computer by:

```shell
cd ColdBox/itsdaq-sw
source ../setup.sh
./INFLUX_DAQ.sh
```

To shutdown ITSDAQ control, use `Ctrl+C`.

### ITSDAQ Configuration
The ITSDAQ configurations are stored inside `~/ColdBox/data`. There are different directories for different setups:

- `testing`: Setup for production modules. (default)
- `training`: Setup for prototype (v0 chipset) modules.

The configuration can be specified as an argument to the `setup.sh` script. If not specified, `testing` is assumed. For example, to use the `training` configuration:
```shell
source ~/ColdBox/setup.sh training
```

## Powerboard and Power Supply Control
The Powerboard and power supply control is done via the powertools package. It can be setup using the same script as ITSDAQ. The powertools configuration is stored inside the `run` directory.
```shell
cd ColdBox/run
source ../setup.sh
```

The main program are for powering up and turning off a module. They control the low voltage and high voltage power supplies. The hybrids are also enabled at the correct times. They assume that there is a powerboard in Chuck 5 and that all positions are loaded (to check per module current). However the commands are sent in parallel to all modules.

To power up a module, run the following from inside `run`:
```shell
pbv3_coldnoise_powerOn -e equip_testbench.json
```

To power down a module, run the following from inside `run`:
```shell
pbv3_coldnoise_powerOff -e equip_testbench.json
```

# Running A Cold Noise Thermal Cycle
The cold noise thermal cycle steps through temperatures from 20C to -30C to 10C in steps of 10C. The full module test is run at each temperature position.

1. Make sure that the box is safe to open (see checklist). Especially that the chiller is at 20C.
2. Open the box.
3. Make sure that the HV and LV power supply outputs are off.
4. Remove caps from the mini-DP connectors.
5. Place modules (testframe and spacer, but without the acrylic covers) on chucks.
6. Fix the modules using four longer screws in the four corners. See Fig 21 in the Cold Testing Specification document.
7. Ground the modules using one shorter screw in the top right corner.
8. Connect the 2x3 molex power cable to the modules. The connector is keyed.
9. Connect the miniDP connectors. The red tagged cable goes to the left (DATA).
10. Close the Cold Box.
11. Turn on dry air (gauge attached on the left side of the box) as high as you can. Typical maximum reading is 15-20 L/min.
13. Wait until Cold Box reaches 1-2%RH. Turn down the dry air for ~8L/min.
15. Power the modules. See "Powerboard and Power Supply Control" for details. The following should be run on the testing computer.

```shell
source ColdBox/setup.sh
cd ColdBox/run
pbv3_coldnoise_powerOn -e equip_testbench.json
```
16. Run a quick test with ITSDAQ to ensure that all modules are responding. The following should be run on the testing computer to start the ITSDAQ GUI. Run the "Full Test" hidden under one of the menus (check the name and edit).
```shell
source ColdBox/setup.sh
cd ColdBox/itsdaq-sw
./RUNITSDAQ.sh
```
17. After closing ITSDAQ, start ITSDAQ in DAQ mode by running the following in the **same** terminal.
```shell
./INFLUX_DAQ.sh
```
18. Navigate to the [Cold Box GUI](http://eplpl004:5000) and click "Start TC" to start thermal cycling.
19. Once thermal cycling completes, shut down `RUNDAQ.sh` with `Ctrl+C`.
20. Power down the modules.
```shell
source ColdBox/setup.sh
cd ColdBox/run
pbv3_coldnoise_powerOff -e equip_testbench.json
```
21. Set chiller to 20C.
22. Once chiller is warm (>10C), you can start removing modules.