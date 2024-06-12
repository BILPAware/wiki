# MadGraph5_aMC@NLO for Muon Colliders

A collection of references and tips for using [MadGraph5_aMC@NLO](https://launchpad.net/mg5amcnlo) to generate collision events at a Muon Collider.

This is not a tutorial on using MadGraph5_aMC@NLO. Other excellent resources exist.

## Resources
- [Madgraph5 aMC@NLO simulation for the muon collider](https://indico.cern.ch/event/801616/contributions/3358582/attachments/1827532/2991430/muon_mg5.pdf) by Xiaoran Zhao

## Setting Up Software

Standalone aMC@NLO works out of the box on the cluster computers. However the the aMC@NLO + Pythia 8 + Delphes + ExROOTAnalysis chain needs to be run inside a container. This is due to missing dependencies on our computers. The ATLAS Alma9 container with and LCG view from CVMFS works.

The ATLAS Alma9 container can be started with the following command. All future command should be run inside of it.

```shell
apptainer shell --cleanenv -B/disk/moose -B/cvmfs /cvmfs/unpacked.cern.ch/registry.hub.docker.com/atlasadc/atlas-grid-almalinux9:latest
```

Setup a recent LCG view and start aMC@NLO. This needs to be run at the start of every session.

```shell
export ATLAS_LOCAL_ROOT_BASE=/cvmfs/atlas.cern.ch/repo/ATLASLocalRootBase
source ${ATLAS_LOCAL_ROOT_BASE}/user/atlasLocalSetup.sh;
lsetup "views LCG_105b x86_64-el9-gcc13-opt"
```

Start aMC@NLO and install the necessary tools.

```shell
./bin/mg5_aMC
install pythia8
install Delphes
install ExRootAnalysis
```


## Example

The following commands will generate events for Higgs production via W scaterring.

```
generate mu+ mu- > h vl vl~
output PROC_mumuWWh
launch
```

Hit `<enter>` when asked about post-processsing programs. Then use option 2 to edit the `run_card.dat`. Ensure that the following fields are set. The `lpp#` value of `0` disables PDFs and `ebeam#` sets the energy of each beam. The following corresponds to a 10 TeV muon collider.

```
0        = lpp1    ! beam 1 type 
0        = lpp2    ! beam 2 type
5000.0     = ebeam1  ! beam 1 total energy in GeV
5000.0     = ebeam2  ! beam 2 total energy in GeV
```

Close the editor and hit `<enter>` to continue.

## Example with EW PDFs
It should be possible to use EW PDFs to generate events. This is appropriate for VBF processes where one parametrizes the probabilty of a muon to emit a vector boson. Similarly to how one parametrizes the hadronic content of a proton. However I haven't managed to get the following to run.

```
set group_subprocesses false
generate w+ w- > h
output PROC_WWh
launch
```

Hit `<enter>` when asked about post-processsing programs. Then use option 2 to edit the `run_card.dat`. Ensure that the following fields are set. The `|lpp#|` value of `4` sets colliding beams to be muons and `ebeam#` sets the energy of each beam. The following corresponds to a 10 TeV muon collider.

```
-4        = lpp1    ! beam 1 type 
4        = lpp2    ! beam 2 type
5000.0     = ebeam1  ! beam 1 total energy in GeV
5000.0     = ebeam2  ! beam 2 total energy in GeV

eva    = pdlabel     ! PDF set Effective W/Z/A Approx
```

Close the editor and hit `<enter>` to continue.

This results in a crash with the following error.

```
DiscreteSampler:: Error, no point could be picked with random variable 0.2365935444831848 using upper bound found of NaN.
```
