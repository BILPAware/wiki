# Introduction
This document describes the local setup of the cold jig software. Generic
documentation is available under the
[ColdJigDCS wiki](https://gitlab.cern.ch/groups/ColdJigDCS/-/wikis/home).

# GrafAna Dashboards
The GrafAna dashboards are only accessible from the desktop computers. Remote
access is documented under
[Accessing the System](http://www.ep.ph.bham.ac.uk/index.php?page=guide/access)
section of the Bham PP computing wiki.

- [ColdJig](http://eplvm003:3000/d/buq47AcVk/uk_china_coldjig_dashboard_flux?orgId=1&refresh=5s)
- [AMAC](http://eplvm003:3000/d/JKm4gvAVk/amac_dashboard_flux?orgId=1&refresh=5s)

# Computers
All computers are only accessible from the `eprexb` gateway. See
[Accessing the System](http://www.ep.ph.bham.ac.uk/index.php?page=guide/access)
for more information.

- `epldt116`: DAQ computer for running ITSDAQ. It uses the same file system and
authentication as the group desktop computers. A local `itkuser2` is available
for production testing.
- `eplpl004`: Raspberry Pi computer for control of the coldjig and running the
ColdJig GUI. A common user, `pi`, should be used by everyone.

Note that the `eplpl004` computer is only accessible via the `eprexb` gateway.
One needs to create a remote SSH tunnel on the GUI port (`5000`) to access it.
The following command should be executed on `eprexb` to access the GUI via a
browser on any of the group desktop computers.

```shell
ssh -R 5000:eplpl004:5000 epldt116 # replace epldt116 with your desktop
```
