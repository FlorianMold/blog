**Table of contents**
- [Setup Intellij in WSL](#setup-intellij-in-wsl)
  - [Install xfce4](#install-xfce4)
    - [Start the desktop:](#start-the-desktop)
    - [Install Intellij](#install-intellij)
  
# Setup Intellij in WSL

## Install xfce4

```bash
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install xfce4
```

### Start the desktop:

`VcXsrv` has to running.

```powershell
startxfce4
```

### Install Intellij

First install the **Jetbrains Toolbox** from https://www.jetbrains.com/toolbox-app/. Inside the toolbox install Intellij IDEA.

Inside the toolbox enable the generation of shell scripts. Set the path for the shell scripts to `~/bin`.

Add the following to `~/.bashrc`:
```bash
export PATH=$HOME/bin:$PATH
```

Afterwards run 
```bash
source ~/.bashrc
```

Now the command `idea &` should start **Intellij IDEA**.

