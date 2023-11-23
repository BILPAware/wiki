# ROOT
[ROOT](https://root.cern.ch/) is the common framework used for analyzing data inside particle physics environments. It contains tools for storing data, visualizing results, statistical tests and many other common tasks.

For new users:

- [Getting Started Guide](https://root.cern/get_started/): Start here to familiarize yourself ROOT.
- [Unofficial ROOT tutorial on YouTube](https://www.youtube.com/playlist?list=PLJZI0Nq8pgrScd_mR_ruxXD7N8dxFZtXv])

One you understand the basics:

- [ROOT Manual](https://root.cern/manual/): Extensive manual about all ROOT functionality.
- [ROOT Tutorials](https://root.cern/doc/master/group__Tutorials.html): The tutorials contain examples of common workflows.
- [Reference Guide](https://root.cern/doc/master/): ROOT API documentation. Class functions are described in details here.

## ROOT and Python
There are two ways to interact with ROOT files in Python. Either using the official ROOT bindings (PyROOT) or by using popular Python libarires and [uproot](https://uproot.readthedocs.io) to open files.

### PyROOT
These are the official python bindings for ROOT. They are just a Python wrapper around the C++ ROOT.

- [Official PyROOT tutorial](https://root.cern/doc/master/group__tutorial__pyroot.html)

### uproot
This is a lightweight implementation of the ROOT I/O with a more modern API. It is designed as Python-first and interacts libraries that most students might already know from courses (ie: matplotlib for plotting).

- [Tutorial](https://masonproffitt.github.io/uproot-tutorial/)

## Tips and Tricks
- [ROOT File Viewer VS Code extension](https://marketplace.visualstudio.com/items?itemName=albertopdrf.root-file-viewer#:~:text=ROOT%20File%20Viewer%20allows%20you,no%20local%20ROOT%20installation%20required): Allows you to open ROOT files directly inside VS Code.