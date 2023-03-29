# Production Setup

This guide is for individuals working on developing the coldjig software. For
production testing, there is a common and stable setup that should be used
instead.

# Repositories

The developement workflow is based on a branch of the official source code. The 
branch includes changes that follow a more typical python flow, namely implement
a `setup.py` to make the packages `pip install`'able. This makes their
installation in test environments much easier. However one needs to cherry-pick
changes to a different branch, based on `master`. before making a merge request.

This is rather annoying and non-ideal. But it does make life easier when testing
custom changes. Attempts are being made to merge this into the main branch. 

The official repositories are under the
[ColdJigDCS group](https://gitlab.cern.ch/ColdJigDCS).

The forks are under [kkrizka](https://gitlab.cern.ch/kkrizka), with packages
published to
`https://gitlab.cern.ch/api/v4/projects/144235/packages/pypi/simple`.

# Installation

Read through the [local instructions](local.md) to understand how to access the
system.

The following commands should be run in your own directory on `eplpl004`. This
is due to the common username. In this case, the example will be `~/mydevel`.

```shell
mkdir ~/mydevel
cd ~/mydevel
```

Create a virtual environment for the packages using `pipenv` and activate it. It
will mainly create a `Pipfile` where you can add the external repositories.

```shell
pipenv shell
```

Open the `Pipfile` and add the following to register the custom index with the
coldjig packages.

```
[[source]]
name = "ColdJigDCS"
url = "https://gitlab.cern.ch/api/v4/projects/144235/packages/pypi/simple"
verify_ssl = true
```

Install the packages. The two main ones are `coldjiglib2` (library for control
of the coldjig) and `coldbox-controller-webgui` (web interface). The `uk` option
install packages specific to the UK hardware.

```shell
pipenv install 'coldjiglib2[uk]' coldbox-controller-webgui --index=ColdJigDCS
```
