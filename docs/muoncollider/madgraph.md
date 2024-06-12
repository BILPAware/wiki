# MadGraph5_aMC@NLO for Muon Colliders

A collection of references and tips for using [MadGraph5_aMC@NLO](https://launchpad.net/mg5amcnlo) to generate collision events at a Muon Collider.

This is not a tutorial on using MadGraph5_aMC@NLO. Other excellent resources exist.

## Resources
- [Madgraph5 aMC@NLO simulation for the muon collider](https://indico.cern.ch/event/801616/contributions/3358582/attachments/1827532/2991430/muon_mg5.pdf) by Xiaoran Zhao

## Setting Up Software

Standalone aMC@NLO works out of the box on the cluster computers. Start aMC@NLO and install the necessary tools.

```shell
git clone git@github.com:mg5amcnlo/mg5amcnlo.git
cd mg5amcnlo
git checkout -b v3.5.4 v3.5.4
export ROOTSYS=/usr
./bin/mg5_aMC
install pythia8
install Delphes
```

Then to start MadGraph in the future, run the following inside the `mg5amcnlo` directory.

```shell
export ROOTSYS=/usr
./bin/mg5_aMC
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
