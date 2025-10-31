This repository documents use of the elephant robotics mycobot 280pi with ubuntu 22.04 and ros jazzy.
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
