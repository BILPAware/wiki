# ASIC Assembly
The ASIC assembly is done by code stored in the directory:

```
/home/itkuser2/hybrid_and_module_building/asic_assembly
```

(which I’ll call $A from now on.) It uses some python scripts which read in a root file (from the hybrid electrical testing), and use information from that root file to find out which ASICs are physically assembled to the hybrids on that panel, and then assemble those ASICs in the database.

This directory has two sub-directories: **asic_assembly_root_files** and **asic_assembly_scripts**.

**asic_assembly_root_files** is the directory where the root files should be saved. Once you get the root file for a panel, you should move it here (and remember of make a note of which file corresponds to your panel!)

**asic_assembly_scripts** is the directory containing the code used for assembling the ASICs. The code we use is actually embedded deep in a sub-directory (*$A/asic_assembly_scripts/strips/modules*) but there’s a handy link in $A which will take you straight there (`cd link_to_scripts`).

Once you’re in the directory with the code in, all you need to do is run the script *do_assemble_asics_bhm.sh*:

```
source do_assemble_asics_bhm.sh
```

You will then be asked to input the path to your root file, which is of the form:

```
/home/itkuser2/hybrid_and_module_metrology/asic_assembly/asic_assembly_root_files/[filename]
```

Note that tab-complete probably won’t work here, so you may need to copy-paste bits of the path if you don’t want to type out the whole thing!
You’ll also be asked the serial number of the **panel** you’re doing the ASIC assembly of, and your itk database credentials – just input these, and the assembly should be good to go!
The script outputs a **lot** of information to the command line, and there’s no way you’ll be able to read and process it all. Instead, just double-check the hybrids on the panel using the link outputted on the last line of the output.