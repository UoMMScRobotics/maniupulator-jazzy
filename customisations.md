The starting point was a standard ubuntu 22.04 64-bit easpberry pi desktop image,
The following steps were taken to customise the image and make it suitable for
use with the maniupulator arm.

* Set up the pi with an internet connection and ensure time is synced
  (you can force a time sync with systemctl restart systemd-timesyncd.service)
* install updates
* install ros jazzy binaries per https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html
* install extra ros packages with sudo apt install ros-jazzy-xacro ros-jazzy-joint-state-publisher-gui
* install pip with sudo apt install python3-pip
* install midnight commander with sudo apt install mc
* install pibootctl with sudo apt install pibootctl
* install pymycobot with pip install pymycobot --upgrade --user --break-system-packages
* make sure the correct /boot/firmware is mounted, if you have another ubuntu image in a SD card reader in your pi it may well mount the wrong one!
* enable the serial port with sudo pibootctl set serial.enabled=1
* set the AMA uart as primary, leaving the miniuart for bluetooth with sudo pibootctl set serial.uart=0
* add your user to the "dialout" group
* reboot the pi
* create a directory ~/colcon_ws and a subdirectory called source and change to it
* clone the mycobot_ros2 repository and make sure the "humble" branch is checked out (there does not seem to be a specific branch for jazzy at this time)
* navigate up to the colcon_ws directory
* run colcon build --symlink-install
