# myKINOVA_ROS
Setting up ROS KORTEX

## Build ROS2 Kortex
1. Source setup.bash
```console
source /opt/ros/humble/setup.bash
```
2. Follow the instructions in "Getting started" in https://github.com/PickNikRobotics/ros2_kortex/tree/main
3. 

## Set up WSL on Windows
1. Install Ubuntu 18.04/22.04 via WSL on Windows
2. Restart Ubuntu and ensure that Systemd is running via ``sudo systemctl status``. If not, run
```console
sudo systemctl reset-failed
```
3. Run ``sudo apt update``
4. Block ACPI features, which cause issues in WSL2, from being installed with Gnome
```console
sudo apt-mark hold acpid acpi-support
```
5. Install ubuntu-desktop and xrdp
```console
sudo apt install ubuntu-desktop xrdp
```
6. Optionally, back up the default config
```console
sudo cp /etc/xrdp/xrdp.ini /etc/xrdp/xrdp.ini.bak
```
7. Windows Pro and higher are often already running RDP on 3389, Prevent conflicts:
```console
sudo sed -i 's/3389/3390/g' /etc/xrdp/xrdp.ini
```
8. Optional if you only have one desktop environment installed
```console
echo gnome-session > ~/.xsession
```
9. Create xsessionrc
```console
vim ~/.xsessionrc
```
with the following contents:
```console
export GNOME_SHELL_SESSION_MODE=ubuntu
export XDG_CURRENT_DESKTOP=ubuntu:GNOME
export XDG_DATA_DIRS=/usr/share/ubuntu:/usr/local/share:/usr/share:/var/lib/snapd/desktop
export WAYLAND_DISPLAY=
export XDG_CONFIG_DIRS=/etc/xdg/xdg-ubuntu:/etc/xdg
```
10. Restart the remote desktop service :
```console
sudo systemctl restart xrdp
```
11. Open a RDP client and tune into ``localhost:3390``.

## To reset WSL
1. List all WSL distributions installed ``wsl --list --all``
2. Delete by ``wsl --unregister Ubuntu-18.04``
3. Reinstall using Microsoft Store

#### Set up Ubuntu16.04 on WSL (needed for kinova ros kortex vision module) - https://aka.ms/wsl-ubuntu-1604

### Misc notes for Ubuntu 18
1. Install tweak for multiple desktops
```console
sudo add-apt-repository universe
sudo apt install gnome-tweak-tool
```
