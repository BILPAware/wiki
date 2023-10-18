# Module Metrology

Similarly, the metrology is run using *module_metrology_test_withfileupload.sh*. Again, we only need to change a couple of lines.

To edit the script, open it in *emacs* using the command:

```
emacs module_metrology_test_withfileupload.sh &
```

If you are working remotely (e.g. at home or in the office) you won’t be able to open *emacs* in a separate window, so you will instead need to run:

```
emacs -nw module_metrology_test_withfileupload.sh
```

Which will open up *emacs* in a command-line window rather than a separate window.

We just need to edit lines 15 and 16, which will read something like this:

```
SENSOR="LS16"
SN="20USBML1234842"
```

These lines determine the directory where we should find the module metrology data, so long as it is of the form:

```
BHM_[CAMPAIGN]_[SENSOR]-[SN]
```

Once you have edited these lines, you should save *module_metrology_test_withfileupload.sh* using *Ctrl-x Ctrl-s*, and then run the script on the command line using:

```
source module_metrology_test_withfileupload.sh
```

If everything goes to plan you will find that, after some running of the analysis, you are asked the question:

```
Do you want to upload results directly to the ITk Production DB? (Y/N)
```

on the command line.

Unless you have already checked the metrology for the module, you should press ‘n’. When you have checked the module metrology and are happy to upload it, you should run the script again and press ‘y’ instead when prompted.