
## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Windows](#windows)
  - [Installing WSL](#installing-WSL)
  - [Install and Setup Debian](#install-and-setup-debian)
  - [Clone the Installation Repo(#clone-the-installation-repo)

## Overview

Get DATUM running in various different setups!

![datum-main](/images/datum-main.png)

---

## Prerequisites

If running X machines - need Y powerful machine
If running Z machines - need A powerful machine

---

## Windows

![windows-0](/images/windows-0.png)

### Installing WSL

1. Open up a PowerShell ![open-powershell](/images/open-powershell.png)
2. Install WSL with `wsl --install` ![install-wsl](/images/install-wsl.png)
3. Hit "Yes" ![yes-1.png](/images/yes-1.png)
4. Restart your machine ![restart-windows](/images/restart-windows.png)

### Install and Setup Debian

1. Open PowerShell again and type `wsl --install -d Debian` ![install-debian](/images/install-debian.png) ![installed-debian](/images/installed-debian.png)
2. Start Debian with `wsl.exe -d Debian` ![exe-debian](/images/exe-debian.png) 
3. It will request a username - here we will use `Bitcoin` ![debian-username-bitcoin](/images/debian-username-bitcoin.png)
4. Enter and retype a password for this user (typed characters will not appear) ![debian-password-retype](/images/debian-password-retype.png)
5. Go root with `sudo -i` ![sudo-i](/images/sudo-i.png)
6. It will request the password you just created ![sudo-enter-password](/images/sudo-enter-password.png)
7. Run `apt update` ![apt-update](/images/apt-update.png)
8. Run `apt upgrade -y` ![apt-upgrade-y](/images/apt-upgrade-y.png)


### Clone the Installation Repo

1. Run `apt install git -y` ![apt-install-git-y](/images/apt-install-git-y.png)
2. Enter `git clone https://github.com/Com320/OC-mech-datum-boxes/` ![git-clone](/images/git-clone.png)
3. Change into the repo with `cd OC-mech-datum-boxes` ![changed-dir](/images/changed-dir.png)
4. Modify the scripts to make them executable with `chmod +x *.sh` ![chmod](/images/chmod.png)
5. Run the installation script with `./main.sh` ![mainsh](/images/mainsh.png)
