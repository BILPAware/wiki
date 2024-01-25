# Introduction
This document describes the local setup of the cold jig software. Generic
documentation is available under the
[ColdJigDCS wiki](https://gitlab.cern.ch/groups/ColdJigDCS/-/wikis/home).

# GrafAna Dashboards
The GrafAna dashboards are only accessible from the desktop computers. Remote
access is documented under
[Accessing the System](http://www.ep.ph.bham.ac.uk/index.php?page=guide/access)
section of the Bham PP computing wiki.

- [ColdJig](http://eprex5:3000/d/buq47AcVk/uk_china_coldjig_dashboard_flux?orgId=1&refresh=5s)
- [AMAC](http://eprex5:3000/d/JKm4gvAVk/amac_dashboard_flux?orgId=1&refresh=5s)

# Computers
All computers are only accessible from the `eprexb` gateway. See
[Accessing the System](http://www.ep.ph.bham.ac.uk/index.php?page=guide/access)
for more information.

- `epldt116`: DAQ computer for running ITSDAQ. It uses the same file system and
authentication as the group desktop computers. A local `itkuser2` is available
for production testing.
- `eplgw1`: Another gateway isolating non-standard computing setups from rest of the
network. Explicit access has to be requested.
- `bpapi004`: Raspberry Pi computer for control of the coldjig and running the
ColdJig GUI. A common user, `pi`, should be used by everyone. SSH access is only
posssible through the `eplgw1` gateway. The WebGUI port (`5000`) is being forwarded
and accessible from all PP cluster computers.