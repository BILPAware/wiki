# Connection to remote host inside remote host (SSH) on VS Code

This short guide explains how to develop on the remote machine in the external network using VS Code. Let's say we need to remotely work on the computer located at CERN. Usually we need to connect to lxplus by `ssh username1@lxplus.cern.ch` and then SSH again to the computer in CERN network `ssh username2@machine-name` allowing for working only in terminal. But what if we want to work with some sophisticated project and to use VS code for that? 

This is the instruction how to establish connection in this case to `tdcpix-testbench` computer in CERN network.

## On your machine

1. Install [Remote-SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) extension on VS Code

2. Create/open `~/.ssh/config` using any text editor you like

3. Write/append these lines (username1 - for login to lxplus, username2 - for login to dedicated machine in CERN network. lxplus, gtk and tdcpix-testbench are just examples):

```config
Host lxplus
    HostName lxplus.cern.ch
    User username1
    IdentityFile ~/.ssh/lxplus_key

Host gtk
    HostName tdcpix-testbench
    User username2
    IdentityFile ~/.ssh/gtk_key
    ProxyJump lxplus
```

## On VS Code 

1. If you did everything right, just press `Ctrl + Shift + P` and start typing `Remote-SSH: Connect to Host`

2. From the dropdown menu choose `tdcpix-testbench` and enter passwords (first password is for connection to the main host (lxplus))

3. Open project folder, enjoy.

NB you can start terminals in VS Code, they are all will be SSHed to the remote machine.

This is the minimum you need to establish connection. If you want to make your life even easier you could generate keys for SSH conncetion and copy them to the remote host/your local machine in order to avoid entering passwords each time
