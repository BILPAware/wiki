# Constructing a Sentaurus TCAD and Allpix Squared Sensor Simulation

## Introduction:

Included here is a TCAD tutorial using the Sentuarus Workbench (SWB) to simulate a series of increasingly sophisticated semiconductor sensors. Following this is an Allpix Squared tutorial for checking sensor functionality, demonstrated using a 224 x 512 pixel matrix with a test beam of pions.

## Preliminary Set-Up for SWB:

### Downloading SWB:

First the TCAD installer must be installed:

`/disk/moose/general/TCAD/downloads/`

Install SynopsysInstaller_v5.7.run by running

`./SynopsysInstaller_v5.7.run`

Copy the downloads to a directory where you have write permissions.In the installed location of the installer.To install using installer, run the following inside where you installed the installer:

`./installer -gui`

Side ID Number: **7789/disk/moose/general/TCAD/downloads**

Select the location of the product that you want to install under the "Source" window. For example,

`/disk/moose/general/TCAD/downloads/tcad_sentaurus_vV-2024.03`

Ignore the not writable error and select the installation location. Now SWB should be installed on your system.

## Loading SWB:

Start up the terminal and apply the following lines to set the license:

`export SNPSLMD_LICENSE_FILE=27020@eplsv004`

`export STROOT=/scratch/synopsys/sentaurus/current/`

cd into the directory containing Sentaurus:

`cd ${STROOT}/bin/`

Then open TCAD SWB:

`./swb`

## Constructing an Initial SWB PN Junction:

The TCAD Sentaurus Tutorial can be found at:

<file:///scratch/synopsys/sentaurus/V-2024.03/tcad/V-2024.03/Sentaurus_Training/index.html>

I would recommend reading the first module up to Section 6 (Managing Projects) to gain an idea of how to use SWB. Pay particular attention to mentions of Device Simulation, as this what we will use to measure the simulated sensor's electrical properties.

## Preliminary Set-Up for Allpix:

Allpix Squared will be used for the Monte Carlo simulation of charge carriers in the sensor modules. Given the failure of the SDE 3D rendering, we will now move onto learning the Allpix basics found at: <https://allpix-squared.docs.cern.ch/docs/>. To open Allpix Squared, you must first move to the directory containing your Allpix configuration files (This can be your home directory). Then type the following command into the command line:

`apptainer shell [docker://gitlab-registry.cern.ch/allpix-squared/allpix-squared](docker://gitlab-registry.cern.ch/allpix-squared/allpix-squared)`

`apptainer shell /cvmfs/unpacked.cern.ch/gitlab-registry.cern.ch/allpix-squared/allpix-squared:latest/` .

I would recommend starting by looking at the **example.conf** and **example_detector.conf** configuration files given in:

`cd allpix-squared/examples/` .

**example_detector.conf** gives an example of how to set up a detector's position and orientation. In this case, the type of detector is cmsp1, the design of which can be found at:

`cd allpix-squared/models/cmsp1`

![](images/Example_Detector.png)

**example.conf** describes how to initialise a simulation of 10000 events, each of which producing a 120GeV 10$\mu$m pion beam.

![](images/Screenshot%20from%202024-07-10%2010-01-24.png)

To start a full simulation, cd into the directory containing the relevant .conf file. To run the file (e.g. to run **example.conf**), type:

`allpix -c <file.conf>` .

Once this has run, now look for the output folder in the same directory as \<file.conf\>. If this is present, you can examine the files in the ROOT Object Browser using:

`root`

`new TBrowser`

Then navigate to the examples folder. You have now demonstrated Allpix Squared functionality. With this in mind, we can now move on to building our own sensor based on the Allpide model.

## Constructing a Sensor Test Beam Simulation

To begin with, we take the Allpide model from the featured Allpix models and change the relevant parameters to match those in the table below.

| Name             | Value           | Unit       |
|------------------|-----------------|------------|
| Sensor Dimension | 20 x 10         | mm$^2$     |
| Pixel Pitch      | 36.4 x 36.4     | $\mu$m$^2$ |
| Pixel Matrix     | 512 x 224       |            |
| Sensor Thickness | 100             | $\mu$m     |
| Sensor Excess    | 0.6816 x 0.9232 | mm$^2$     |

: Table of Sensor Parameters

You will then need to add the following line in the main simulation configuration file:

`model_paths = "./allpix-squared/<detector_files>/"`

Where \<detector_files\> is the directory where allpide is stored. This allows Allpix to know where you want it to check for pre-defined detectors.

UNEDITED BELOW:

Sentaurus Process can be used for fabrication, while Sentaurus Structure Editor uses pre-defined geometries. After a structure is generated, we can create a device to measure the electrical properties. To extract values from the simulation, the simulation flow must end with a Sentaurus Visual.

NOTE: Sentaurus Workbench (SWB) comes with pre-prepared projects.

Sentaurus Interconnect potential usage for multiple connected components

Sentaurus Project tab organised from top to bottom as: Total Flow (SPROCESS, SDEVICE, SVISUAL), Project Parameters, Simulation Tree.

Nodes in the Simulation Tree contain data.

SWB projects can be organised in two ways: \* Hierarchical: core project files, and simulation results are separated \* Traditional: all project data is placed in one directory

Parallel processing will be required if a 3D simulation is constructed.

Decided to move on from Sentaurus Workbench tutorial after Section 6. Now working on to Sentaurus Structure Editor module.Can return to previous module for advice on Sentaurus preferences.

To start Sentaurus Structure Editor on the command line, type: ./sde (same as for ./swb).

To start Sentaurus Visual, type: ./svisual. Could use the Plot Overlay function in Sentaurus Visual to compare the behaviour of the simple PN junction to the rudimentary sensor module.

Sentaurus Visual command prompts can be written in tool command language (TCL) and/or python. A tutorial for this is included in the main Sentaurus tutorial. For the purposes of debugging, a knowledge of TCL basics is recommended.

NOTE: Allpix Squared also provides the possibility to utilize a full electrostatic TCAD simulation for the description of the electric field.

Root tutorial found at: <https://root.cern.ch/root/htmldoc/guides/users-guide/Trees.html>

To look for histogram data, go to PixelHit/\<detector\>/pixel/local_center\_/X()
