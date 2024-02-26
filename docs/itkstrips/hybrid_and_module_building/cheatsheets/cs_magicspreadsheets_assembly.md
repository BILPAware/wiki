# Guide to Gluing/Assembly Shell Scripts:

| Script | Use | Description |
| ------ | --- | ----------- |
| `run_assembly_hybrids_bhm.sh` | Hybrid Gluing and Panel Assembly | Creates a new Hybrid Assembly. Assembles the Flex to the Hybrid Assembly using the Flex Code. Uploads a Glue Weight Test to the Hybrid Assembly. Assembles the Hybrid Assembly to a Hybrid Panel(WIP). |
| `run_assembly_modules_bhm.sh` | LS Module Gluing | Assembles a Hybrid to the LS Module. Assembles a Powerboard to the LS Module. Uploads a Hybrid/PB Glue Weight Test to the LS Module. Moves LS Module to `GLUED` stage. |


# Quick-Start Guide

We will use `run_assembly_hybrids_bhm.sh` as our example, but the same process applies to all Magic Spreadsheets.

## Open Shell Script in GNU EMacs:
```
emacs run_assembly_hybrids_bhm.sh &
```

## Edit Line 
Edit Line starting with `python`, to match the sheet, tab, credentials, column and batch you are using, e.g.:
```
python ./run_hybrids.py -s "BHM_Hybrid_Assembly_410umFlex" -t "P30_Use1" -c "/home/rb/Documents/ITk/ItKDB/cam_itk/credentials/credentials.yml" -l "C" -b "OTHER"
```

## Save Shell Script
Use `Ctrl-X Ctrl-S` to save the script in Emacs after editing it.

## Close Emacs
Use `Ctrl-X Ctrl-C` to close Emacs

## Run Shell Script
Run the script using the `source` command in the linux terminal, e.g.
```
source run_assembly_hybrids_bhm.sh
```

## Check Output
Watch the logging output for `WARNING` messages, which usually appear in purple.

`WARNING` messages which say something like `Logger not passed to SOMETHING` aren't a worry, it's a minor bug which doesn't affect the uploads.

Other `WARNING` messages indicate something wrong in the code or with the Google Sheets, most often that something in the Google Sheets isn't quite right. Just check the spreadsheet for the error, fix it, and re-run.