# Metrology

## Upload Metrology Data

To upload metrology data to moose, you should take the memory stick and insert it into the ALMA9 PC (the one next to the wire bonders). Open up a file explorer, and locate the metrology repository on moose. There are several ways of doing this:

1. In the File Explorer, find the left-hand shortcuts bar, and click on "Favourites." You should find links to the moose repository in there.

2. In the File Explorer, find the left-hand shortcuts bar, and click on "Home." You should find links to the moose repository in there.

3. In the File Explorer, navigate to */disk/moose/atlas/ITk-production/metrology/[hybrids/modules]*

## Metrology Analysis

The metrology analysis code is stored in the directory:

```
/home/itkuser2/hybrid_and_module_building/metrology
```

(which I’ll call $M from now on), and is split into two parts: hybrid metrology and module metrology. Once the data files have been uploaded to CERNBox, they will be accessible via links in the $M directory, so we don’t need to do any more transferring!

The process of doing the metrology analysis is as follows:

1. Extract the metrology measurements from the .rtf files, and print them into .dat files. This is done in the python script *$M/itk-metrology-scripts/ExtractMeasurements.py*

2. Run analysis of the metrology, printing the results into both a text file (.json) and some plots (.pdf). This is done in the python script *$M/metrologyanalysis_hackyprodbranch/analysis.py*

3. Upload the .json file to the database as a Metrology Test, and attach the .dat file to that test. This is done using the python script *$M/production_database_scripts/upload_test_results.py*, and either *$M/uploadfile_hybrid.py* or *$M/uploadfile_module.py*

We use shell scripts to run all of the above automatically.

# Links

[Hybrid Metrology](./metrology_hybridmetrology.md)

[Module Metrology](./metrology_modulemetrology.md)