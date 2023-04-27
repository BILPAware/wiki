# Production Setup

This guide is for individuals working on developing the coldjig software. For
production testing, there is a common and stable setup that should be used
instead.

# Web Interface
## Repositories

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

## Your Directory

Read through the [local instructions](local.md) to understand how to access the
system.

The following commands should be run in your own directory on `eplpl004`. This
is due to the common username. In this case, the example will be `~/mydevel`.
The log directories are not created by default and the GUI will crash if they
do not exist.

```shell
mkdir ~/mydevel
cd ~/mydevel
mkdir log && mkdir log/webserver
```

## Installation

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

## Package Developement
Make a clone of the package you want to develop and switch to the `setuppy`
branch. Make sure to use the https repository URL as this is a shared account.
Then install the package in editable mode.

For example,
```shell
git clone --branch setuppy2 https://gitlab.cern.ch/kkrizka/coldjiglib2.git
pipenv install -e coldjiglib2/
```

## Starting the Web Interface
A downside of the editable install is that the default configurations are not
installed. Instead use the copy under `/home/pi/configs/config.conf`. If you need
to edit it, make a copy of this directory.

```shell
pipenv run coldbox_controller_webgui.py -c /home/pi/configs/config.conf -v
```

Note that you need to foward the port `5005` to access the web interface on your
computer. See the [local instructions](local.md) for more information. This only
needs to be done once per computer and `epldt116` is most likely already setup.