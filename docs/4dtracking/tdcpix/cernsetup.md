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