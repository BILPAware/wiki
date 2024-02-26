# Guide to Wire Bonding Shell Scripts:

| Script | Use | Description |
| ------ | --- | ----------- |
| `run_wirebonding_hybrids_bhm.sh` | Hybrid Wire Bonding | Checks for prerequisite tests. Moves Hybrid Assembly to the `WIRE_BONDING` stage. Uploads a Wire Bonding Test to the Hybrid Assembly. |
| `run_wirebonding_modules_bhm.sh` | Module Wire Bonding | Checks for prerequisite tests. Moves Module to the `BONDED` stage. Uploads a Wire Bonding Test to the Module. |

# Quick-Start Guide

We will use `run_wirebonding_hybrids_bhm.sh` as our example, but the same process applies to all Magic Spreadsheets.

## Open Shell Script in GNU EMacs:
```
emacs run_wirebonding_hybrids_bhm.sh &
```

## Edit Line 
Edit Line starting with `python`, to match the sheet, tab, credentials, column and batch you are using, e.g.:
```
python ./run_hybrid_wirebonding.py -s "Wirebonding Panels (CrackingSensorsGromit)" -t "P18_Use4_X_P0" -c "/home/rb/Documents/ITk/ItKDB/cam_itk/credentials/credentials.yml"
```

## Save Shell Script
Use `Ctrl-X Ctrl-S` to save the script in Emacs after editing it.

## Close Emacs
Use `Ctrl-X Ctrl-C` to close Emacs

## Run Shell Script
Run the script using the `source` command in the linux terminal, e.g.
```
source run_wirebonding_hybrids_bhm.sh
```

## Check Output
Watch the logging output for `WARNING` messages, which usually appear in purple.

`WARNING` messages which say something like `Logger not passed to SOMETHING` aren't a worry, it's a minor bug which doesn't affect the uploads.

Other `WARNING` messages indicate something wrong in the code or with the Google Sheets, most often that something in the Google Sheets isn't quite right. Just check the spreadsheet for the error, fix it, and re-run.