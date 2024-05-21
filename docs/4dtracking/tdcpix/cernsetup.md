# TDCPix Test Setup at CERN

Instructions for connecting to and using the TDCPix test setup in building 14 at CERN.

## Connecting

The chip is connected to `tdcpix-testbench` available on the CERN network. For outside access, connect via `lxplus`.

### GrafAna

Power supplies and other quantites are being pushed to GrafAna setup on the test computer. To access from outside of CERN, you need to create a tunnel via `lxtunnel`.

```shell
ssh -L 3000:tdcpix-testbench:3000 lxtunnel.cern.ch
```

Point your browser to [http://localhost:3000](http://localhost:3000) or directly the [Monitoring Dashboard](http://localhost:3000/d/adla6sajk91j4c/test-setup?orgId=1&refresh=5s).

## Power Supplies

|Power Supply | Voltage | Current |
|-------------|---------|---------|
| Chip Power (PLL Disabled) | 3.6V | 1.97 A |
| Chip Power (PLL Enabled) | 3.6V | 3.26 A |
| Sensor Bias (Testing) | -10V |  |

## Code

A git repository with the code is available at [https://gitlab.cern.ch/bvelghe/tdcpix-test-bench](https://gitlab.cern.ch/bvelghe/tdcpix-test-bench). A central clone exists in the shared account under `/home/gtk2021/projects/tdcpix-test-bench`.

### Installation

Make sure you have an older version of ROOT (v5.34.38) available under ``. The setup script looks for it in this location. If you do not, you can compile it following:

```shell
git clone https://github.com/root-project/root.git
cd root
./configure --prefix ${HOME}/opt/root_v5.34.38
make
make install
```

Now you can compile the `tdcpix-test-bench` project. Note that you'll have to source the `setup.sh` in every new session when using the testbench. It setups all the necessary paths and configuration variables.

```shell
git clone ssh://git@gitlab.cern.ch:7999/bvelghe/tdcpix-test-bench.git
cd tdcpix-test-bench/
source setup.sh
cd .libs
./mklinks.sh
cd ..
make
```

If everything compiled successfully, you should see executables available under `TDCPixReadOut/Tools/bin/`.

## Running

Always `source setup.sh` inside a new shell to setup all of the necessary paths.

Most of the key DAQ programs are located inside `TDCPixReadOut/Tools/bin/`. All commands below are executed from inside that directory, unless otherwise stated.

The `InterfaceController` must be running at all times. If the DAQ gets stuck, start by restarting it (kill + run again). To start it, run the following and leave it in the background:

```shell
./InterfaceController reset
```

The PLL needs to be enabled when running tests. When no running tests, please disable it (first arugment `0`) as this increases the chip power usage considerably.

```shell
./PLLEnable 1
``