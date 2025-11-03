# Download and flash the image
You can use disks built into ubuntu
<p align="center">
    <img title="disk1" src="../Images/disks.png" width="60%"/>
</p>
<p align="center">
    <img title="disk2" src="../Images/disks_flash.png" width="60%"/>
</p>
<p align="center">
    <img title="disk3" src="../Images/disks_flash_2.png" width="60%"/>
</p>

# Boot the pi 
The user is elephant and has a static IP of `10.3.14.59` and password of `trunk`. If you want to remote access then you can `ssh elephant@10.3.14.59`.
Check the network on the pi, it should be set up as below.
<p align="center">
    <img title="Network" src="../Images/Network.png" width="60%"/>
</p>
<p align="center">
    <img title="Network" src="../Images/Network_mani_pi.png" width="60%"/>
</p>

# Update the bashrc of the pi
**ROS2 Environment Setup:**  
   We can automate sourcing our ROS workspace by appending instructions to **the end of** the `.bashrc` script.

 ```
 nano ~/.bashrc
 ```
 Scorll down to the bottom of the file and add:
 Ensure you replace `YOUR_GROUP_NUMBER' with an int value.
 ```bash
 # Source ROS Jazzy setup with error checking
if source /opt/ros/jazzy/setup.bash; then
  echo "Sourced /opt/ros/jazzy/setup.bash successfully"
else
  echo "Failed to source /opt/ros/jazzy/setup.bash"
fi

# Explicit setting of DDS
export RMW_IMPLEMENTATION=rmw_fastrtps_cpp
echo "DDS set to $RMW_IMPLEMENTATION"

# Source your workspace setup with error checking
if source ~/colcon_ws/install/setup.bash; then
  echo "Sourced ~/colcon_ws/install/setup.bash successfully"
else
  echo "Failed to source ~/colcon_ws/install/setup.bash"
fi

# Export and print ROS_DOMAIN_ID
export ROS_DOMAIN_ID=YOUR_GROUP_NUMBER
echo "ROS_DOMAIN_ID is set to $ROS_DOMAIN_ID"

# ROS_LOCALHOST_ONLY is being fazed out but is good for a quick set up
export ROS_LOCALHOST_ONLY=0
echo "ROS_LOCALHOST_ONLY is set to $ROS_LOCALHOST_ONLY"

echo "To change this automation, use nano to edit ~/.bashrc and the source ~/.bashrc to apply."
 ```
 Exit nano (CTRL+X) and save.

 After saving, apply the changes by running:
 ```bash
 source ~/.bashrc
 ```
 This ensures your environment variables.
 
 **Test Servos:**  
 Launch the slider test:
 ```bash
 ros2 launch mycobot_280pi slider_control.launch.py
 ```
> [!WARNING]
> Avoid using the `Randomize` button. This interface does not contrain the manipulator. Random joint configurations may cause the arm to attempt to move through the table or other objects.
---

# Set up your laptop/NUC
We're doing a wired peer to peer network using static IPs.
Set up the laptop with the below.
<p align="center">
    <img title="disk3" src="../Images/Network_Laptop.png" width="60%"/>
</p>
If you previously set up a network config with the previous guidance run the below
```
sudo rm /etc/netplan/99-wired-static.yaml
sudo netplan apply
```

You'll also need to update the bashrc of the laptop

```
# Source ROS Jazzy setup with error checking
if source /opt/ros/jazzy/setup.bash; then
  echo "Sourced /opt/ros/jazzy/setup.bash successfully"
else
  echo "Failed to source /opt/ros/jazzy/setup.bash"
fi

# Delcare the DDS
export RMW_IMPLEMENTATION=rmw_fastrtps_cpp
echo "Explicilty set fast DDS"


# Export and print ROS_DOMAIN_ID
export ROS_DOMAIN_ID=10
echo "ROS_DOMAIN_ID is set to $ROS_DOMAIN_ID"
echo "To change this automation, use nano to edit ~/.bashrc and the source ~/.bashrc to apply."

# For quick setup use ROS_LOCALHOST_ONLY, do revise later
export ROS_LOCALHOST_ONLY=0
echo "ROS_LOCALHOST_ONLY set to zero"
```
Then update by sorcing
```
source ~/.bashrc
```

# Almost there
Now theoretically speaking you should be able to run ` ros2 launch mycobot_280pi slider_control.launch.py` on the raspberry pi and then do `ros2 topic list` on your laptop and see the topics from your laptop.

---

This repository documents use of the elephant robotics mycobot 280pi with ubuntu 24.04 and ros jazzy.
This is more up to date than the ubuntu 22.04/ros humble setup that elephant ship, and provides a
cleaner environment where everything is in english.

A ready-prepared image will be made available to students, details are pending.
The ethernet port has been configured to use a static IP address of 10.3.14.51,
the username is elephant and the default password is trunk.

For more information on how the image was customised see customisations.md

The elephant robotics ros packages have been cloned on the image in
/home/elephant/colcon_ws and built. These packages were intended for ros
humble but they seem to work with ros Jazzy.

However, having looked at these packages, I would regard them more as 
"example code" than as ready to use nodes. 

You can run the example with the following stesp

* Change to ~/colcon_ws
* run ". /opt/ros/jazzy/setup.bash" to bring ros jazzy into scope.
* run ". install/setup.bash" to bring the mycobot ros packages into scope
* run "ros2 launch mycobot_280pi slider_control.launch.py"
