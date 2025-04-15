
## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Windows](#windows)
  - [Installing WSL](#installing-WSL)
  - [Install and Setup Debian](#install-and-setup-debian)
  - [Clone the Installation Repo](#clone-the-installation-repo)
  - [Install Bitcoin Knots and Datum](#install-bitcoin-knots-and-datum)
  - [Configuring systemd](#configuring-systemd)
  - [Networking](#networking)
  - [Run WSL at Startup](#run-wsl-at-startup)
- [Debian](#debian)
  - [Install Git and Clone the Installation Repo](#install-git-and-clone-the-installation-repo)
  - [Run the Installation Scripts](#run-the-installation-scripts)

## Overview

Get DATUM running in various different setups!

![datum-main](/images/windows-images/datum-main.png)

---

## Prerequisites

If running X machines - need Y powerful machine
If running Z machines - need A powerful machine

---

## Windows

![windows-0](/images/windows-images/windows-0.png)

### Installing WSL

1. Open up a PowerShell ![open-powershell](/images/windows-images/open-powershell.png)
2. Install WSL with `wsl --install` ![install-wsl](/images/windows-images/install-wsl.png)
3. Hit "Yes" ![yes-1.png](/images/windows-images/yes-1.png)
4. Restart your machine ![restart-windows](/images/windows-images/restart-windows.png)

### Install and Setup Debian

1. Open PowerShell again and type `wsl --install -d Debian` ![install-debian](/images/windows-images/install-debian.png) ![installed-debian](/images/windows-images/installed-debian.png)
2. Start Debian with `wsl.exe -d Debian` ![exe-debian](/images/windows-images/exe-debian.png) 
3. It will request a username - here we will use `Bitcoin` ![debian-username-bitcoin](/images/windows-images/debian-username-bitcoin.png)
4. Enter and retype a password for this user (typed characters will not appear) ![debian-password-retype](/images/windows-images/debian-password-retype.png)
5. Go root with `sudo -i` ![sudo-i](/images/windows-images/sudo-i.png)
6. It will request the password you just created ![sudo-enter-password](/images/windows-images/sudo-enter-password.png)
7. Run `apt update` ![apt-update](/images/windows-images/apt-update.png)
8. Run `apt upgrade -y` ![apt-upgrade-y](/images/windows-images/apt-upgrade-y.png)


### Clone the Installation Repo

1. Install git by running `apt install git -y` ![apt-install-git-y](/images/windows-images/apt-install-git-y.png)
2. Clone the repo with `git clone https://github.com/Com320/OC-mech-datum-boxes/` ![git-clone](/images/windows-images/git-clone.png)


### Install Bitcoin Knots and Datum

1. Change directory into the repo with `cd OC-mech-datum-boxes` ![changed-dir](/images/windows-images/changed-dir.png)
2. Modify the scripts to make them executable with `chmod +x *.sh` ![chmod](/images/windows-images/chmod.png)
3. Run the installation script with `./main.sh` ![mainsh](/images/windows-images/mainsh.png)

**The installation script will now run and the configuration files for Bitcoin Knots and DATUM will be generated requesting your input along the way. The configuration files can be modified later if desired.**

4. Once the script has successfully been run, you will see the following ![finished-script](/images/windows-images/finished-script.png)
5. You will now begin syncing the Blockchain - you can monitor its progress with `tail -f /home/bitcoin/.bitcoin/data/debug.log` ![debug-log](/images/windows-images/debug-log.png)
6. Hit `ctrl C` to stop watching the logs ![ctrl-c](/images/windows-images/ctrl-c.png)

### Configuring systemd

1. Ensure that systemd is configured to run automatically with `cat /etc/wsl.conf` ![cat-wsl-conf](/images/windows-images/cat-wsl-conf.png)
2. Skip to the [Networking](#networking) if you see the above output. If you do not see the output in the above picture:

```
If `systemd=false` change it to "true" by doing the following:
  -  `nano /etc/wsl.conf`
  -  Change "false" to "true"
  -  Hit `ctrl X` then `Y` then `enter` to save the file. 
  
If the file "/etc/wsl.conf" does not exist:
  - `nano /etc/wsl.conf`
  - Then enter the following:
[boot]
systemd=true
  - Hit `ctrl X` then `Y` then `enter` to save the file
```

3. Restart wsl with `wsl.exe --shutdown`
4. Confirm it is working with `systemctl status` ![systemctl-status](/images/windows-images/systemctl-status.png)

### Networking

1. Enter "WSL Settings" ![wsl-settings](/images/windows-images/wsl-settings.png)
2. Click "Networking" and change "Networking mode" to "Mirrored" ![networking-mirrored](/images/windows-images/networking-mirrored.png)
3. Right click on "Terminal" and click "Run as administrator" ![run-as-admin](/images/windows-images/run-as-admin.png)
4. Click "Yes" when asked if you want to allow Terminal to make changes ![terminal-makes-changes](/images/windows-images/terminal-make-changes.png)
5. Enter "wsl --shutdown" ![wsl-shutdown](/images/windows-images/wsl-shutdown.png)
6. Open "Windows Defender Firewall with Advanced Security" ![firewall-advanced](/images/windows-images/firewall-advanced.png)
7. Click on "Inbound Rules" and then "New Rule..." ![inbound-new-rule](/images/windows-images/inbound-new-rule.png)
8. Click "Port" and click "Next" ![port-next](/images/windows-images/port-next.png)
9. Enter "23334" for "Specific local ports" and click "Next" ![23334-next](/images/windows-images/23334-next.png)
10. "Allow the connection" and click "Next" ![allow-next](/images/windows-images/allow-next.png)
11. Under "When does this rule apply?" leave all three enabled and click "Next" ![just-next](/images/windows-images/just-next.png)
12. Name the new rule and click "Finish" ![name-finish](/images/windows-images/name-finish.png)
13. Finally, go back to Terminal and enter `ipconfig /all` and make a note of the IPv4 Address - **this is where you will point your miners** ![ipconfig-all](/images/windows-images/ipconfig-all.png)

**Note: You will want to assign your Windows machine a static IP on your network to ensure that it doesn't change.**  

### Run WSL at Startup

1. Right click on the Windows button ![right-click-start](/images/windows-images/right-click-start.png)
2. Unfurl "Task Scheduler" ![unfurl-task](/images/windows-images/unfurl-task.png)
3. Left click then right click on "Task Scheduler Library" and click "Create Task"
4. Name the task `startWSL` and check "Run whether user is logged on or not" ![name-run-whether](/images/windows-images/name-run-whether.png)
5. Click "Triggers" then "New" ![triggers-new](/images/windows-images/triggers-new.png)
6. Open the "Begin the task" drop down menu and select "At startup" ![at-startup](/images/windows-images/at-startup.png)
7. Click "Actions" then "New" ![actions-new](/images/windows-images/actions-new.png)
8. Click "Browse" ![browse](/images/windows-images/browse.png)
9. Search for "wsl.exe" and click "Open" ![search-wsl-open](/images/windows-images/search-wsl-open.png)
10. Click "OK" ![ok-1](/images/windows-images/ok-1.png)
11. Uncheck "Start the task only if the computer is on AC power" if desired ![uncheck-ac](/images/windows-images/uncheck-ac.png)
12. Copy the below settings - modify as desired ![many-mods](/images/windows-images/many-mods.png)
13. Click "OK", enter your password and click "OK" again ![enter-pass-ok](/images/windows-images/enter-pass-ok.png)

**You can now connect your miners to your DATUM gateway once your node has finished syncing!**


## Debian

### Install Git and Clone the Installation Repo

1. Go sudo with `sudo -i`
2. Run `apt update`
3. Run `apt upgrade -y`
4. Run `apt install git -y`
5. Run `git clone https://github.com/Com320/OC-mech-datum-boxes`
6. Change into the cloned repo `cd OC-mech-datum-boxes`

### Run the Installation Scripts

1. Start by making them executable `chmod +x *.sh`
2. Run `./main.sh`
3. Follow the onscreen prompts to install and configure your Bitcoin Knots node and your DATUM gateway!

**For instructions on how to configure your node/gateway see here.**

**Your node will now sync. Check its progress with `/home/bitcoin/bitcoin/bin/bitcoin-cli getblockcount`**

**You can now connect your miners to your DATUM gateway!**
