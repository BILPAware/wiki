# How To Use a Computer
The following is a list of good resources to get new students started with using common developement tools. We try to use as many standard tools as possible. One should never reinvent the wheel. Especially if they are a physicist.

For a very comprehensive list of available tools, see [Sindresorhus's Awesome List](https://github.com/sindresorhus/awesome).

## GNU/Linux
Most of our software is designed to be run on a Linux computer. Using it is very important.

- [Learning the Shell](http://linuxcommand.org/lc3_learning_the_shell.php)
- [SSH and SCP](https://acloudguru.com/blog/engineering/ssh-and-scp-howto-tips-tricks): Working on a Linux machine remotely.
- [tmux](https://hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/): A multiplexers for manu virtual terminals at a remote (or local) host.

## Programming
- [Learn C++](https://www.learncpp.com/): C++ tutorial recommended by Adam.
- [I don't like notebooks](https://www.youtube.com/watch?v=7jiPeIFXb6U): Great presentation by Joel Grus on why you should **not** use Jupyter Notebooks.

## Build Automation Tools
- [What is a Makefile and how does it work?](https://opensource.com/article/18/8/what-how-makefile): Learn the concept behind makefiles, but use an advanced build tool (like CMake) to generate them.
- [FIRST-HEP CMake3 Tutorial](https://henryiii.github.io/cmake_workshop/)

## Git and Code Versioning
Git is a common and very useful tool for versioning your source code. One's will see a significant improvement to their life if they learn the concepts behind git instead of just blindly copy-pasting commands.

- [Learn Git Branching](https://learngitbranching.js.org/)
- [Getting Started with CERN GitLab - US Computing Bootcamp 2020](https://aroepe.github.io/atlas-gitlab/)

## GDB
The GNU Debugger is a much better debugging tool that `cout` statements.

- [Beej's Quick Guide to GDB](https://beej.us/guide/bggdb/)

## Python Libraries
Tutorial on useful Python libraries for particle physics data analysis.

- [Uproot Tutorial](https://masonproffitt.github.io/uproot-tutorial/): uproot is a lighweight and modern Python library for ROOT I/O

# ATLAS Computing

- [The US ATLAS Computing Bootcamp 2020](https://matthewfeickert.github.io/usatlas-computing-bootcamp-2020/): Set of tutorials designed to get oneself familiar with the computing tools (git, cmake, docker) used by the ATLAS collaboration. Morning lectures focus on the (generic) tool itself. Afternoon lectures focus on how it is used by ATLAS.

# Examples
Useful examples and code snipplets.

- [Doxygen CI](https://gitlab.cern.ch/berkeleylab/labRemote/-/blob/774c91c61cbe7884e8cd455c03620c4c254cc22d/.gitlab-ci.yml#L66): Deploy automatically generated documentation to lxplus