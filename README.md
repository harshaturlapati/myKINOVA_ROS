# myKINOVA_ROS
Setting up ROS KORTEX

### Set up ROS Melodic using http://wiki.ros.org/melodic/Installation/Ubuntu

### Build ROS Kortex using https://github.com/Kinovarobotics/ros_kortex

## Install ROS Kinetic from source on Ubuntu 18
http://wiki.ros.org/kinetic/Installation/Source

## Set up WSL on Windows
1. Install Ubuntu 18.04 via WSL on Windows
2. Restart Ubuntu and ensure that Systemd is running via ``sudo systemctl status``. If not, run ``sudo systemctl reset-failed``
3. Run ``sudo apt update``
4. Block ACPI features, which cause issues in WSL2, from being installed with Gnome
``sudo apt-mark hold acpid acpi-support``
5. Install ubuntu-desktop and xrdp
``sudo apt install ubuntu-desktop xrdp``
6. Optionally, back up the default config
``sudo cp /etc/xrdp/xrdp.ini /etc/xrdp/xrdp.ini.bak``
7. Windows Pro and higher are often already running RDP on 3389, Prevent conflicts:
``sudo sed -i 's/3389/3390/g' /etc/xrdp/xrdp.ini``
8. Optional if you only have one desktop environment installed
``echo gnome-session > ~/.xsession``
9. Create ``~/.xsessionrc`` with the following:
10. 
``export GNOME_SHELL_SESSION_MODE=ubuntu``

``export XDG_CURRENT_DESKTOP=ubuntu:GNOME``

``export XDG_DATA_DIRS=/usr/share/ubuntu:/usr/local/share:/usr/share:/var/lib/snapd/desktop``

``export WAYLAND_DISPLAY=``

``export XDG_CONFIG_DIRS=/etc/xdg/xdg-ubuntu:/etc/xdg``

11. Restart the remote desktop service : ``sudo systemctl restart xrdp``
12. Open a RDP client and tune into ``localhost:3390``.

## To reset WSL
1. List all WSL distributions installed ``wsl --list --all``
2. Delete by ``wsl --unregister Ubuntu-18.04``
3. Reinstall using Microsoft Store

#### Set up Ubuntu16.04 on WSL (needed for kinova ros kortex vision module) - https://aka.ms/wsl-ubuntu-1604
