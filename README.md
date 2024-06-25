# myKINOVA_ROS
Setting up ROS KORTEX

## Set up WSL on Windows
1. Install Ubuntu 18.04/20/22.04 via WSL on Windows
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

## Configure Kinova Kortex Vision in ROS
1. Install [ROS Noetic](https://wiki.ros.org/noetic/Installation/Ubuntu) for Ubuntu 20
2. Get dependencies installed
```console
sudo apt install gstreamer1.0-tools gstreamer1.0-libav libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-good1.0-dev gstreamer1.0-plugins-good gstreamer1.0-plugins-base
```
3. Install ROS package rgbd_launch
```console
sudo apt-get install ros-noetic-rgbd-launch
```
4. Build ros_kortex_vision ([Source](https://github.com/Kinovarobotics/ros_kortex_vision?tab=readme-ov-file#building)) by creating a catkin workspace
```bash
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src/
```
Clone this git repo into `~/catkin_ws/src`
```bash
git clone https://github.com/Kinovarobotics/ros_kortex_vision.git
```
```bash
cd ~/catkin_ws/src/
catkin_init_workspace 
cd ..
catkin_make clean
catkin_make
catkin_make install
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
5. Usage
Start roscore (if not already started)<br />
```bash
roscore
```
Start kinova_vision node<br />
```bash
roslaunch kinova_vision kinova_vision.launch
```
Start rviz to view both cameras<br />
```bash
rosrun rviz rviz
```
## Configure Kinova Kortex in ROS


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
2. Install terminator for multiple terminals
```console
sudo apt install terminator
```
