# Samples for Studies

## Generating Samples

Following the instrucions under [uC MadGraph](/muoncollider/madgraph) on how to setup the full MadGraph chain with a shower and a simplified detector simulation.

The following instructions are targetting a Muon Collider. However the setup should be the same for FCCee, with a change in the initial state.

Generating WW events.

```
generate mu+ mu- > w+ w-, w+ > l+ vl, w- > l- vl~
output PROC_ww
launch
2 # Enable detector output
done
1 # Edit the param card to set the mass of the W
2 # Edit the run card to set the beam energy (5000.0 = ebeam(12) for 10 TeV muon collider)
4 # Edit the delphes card to correspond to a detector at a Muon Collider (use default for now)
done
```

## Sample List

A few test files are copied to the following location. Unclear if the W mass variation was correctly propagated.

```
/disk/moose/general/FutureWMass/samples/
```