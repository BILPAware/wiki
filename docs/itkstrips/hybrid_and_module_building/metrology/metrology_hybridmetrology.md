# Hybrid Metrology
Hybrid metrology analysis is run using *hybrid_metrology_test_withfileupload.sh*. This script is quite long, but don’t worry! We don’t need to change much.
To edit the script, open it in *emacs* using the command:
```
emacs hybrid_metrology_test_withfileupload.sh &
```
If you are working remotely (e.g. at home or in the office) you won’t be able to open *emacs* in a separate window, so you will instead need to run:
```
emacs -nw hybrid_metrology_test_withfileupload.sh
```
Which will open up *emacs* in a command-line window rather than a separate window.
The only thing we need to edit is on line 5, which will read something like:
```
DATA="/home/itkuser2/hybrid_and_module_building/metrology/moose_CrackingStudies_Hybrids/BHM_P10_Use4/"
```
This is a line which tells us which folder to look into to find the metrology data, and is also where we will save the results. Simply edit this line to match the folder with the metrology you want to analyse (you’ll usually only have to edit the ‘BHM_P10_Use4’ bit), then save (*Ctrl-x Ctrl-s*). Then you can run the script on the command line using:
```
source hybrid_metrology_test_withfileupload.sh
```
If everything goes to plan you will find that, after some running of the analysis, you are asked the question ‘Do you want me to upload metrology test results to the database?’ on the command line. Unless you have already checked all the metrology **for the entire panel**, you should press ‘n’. When you have checked all the panel metrology and are happy to upload it, you should run the script again and press ‘y’ instead when prompted.