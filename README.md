# rtabmap_tools
set of launch files to run rtabmap on turtlebot

Just a testing repo

## Environment Setup
```bash
# install turtlebot
# install Joy ps3joy
# install rtabmap
# install respective 3D cam, e.g. Kinect, Xtion, Realsense
```

## Control Turtlebot with Joystick

Here, a ps3 controller is used. Connect ps3 controller with bluetooth. Pls refer to
[here](http://wiki.ros.org/ps3joy#ps3joy_node.py).

Run the node to convert joy input to twist output
```bash
ros_load # alias to load env
roslaunch rtabmap_tools turtlebot_joy_controller.launch
```

Open another terminal to connect the ps3 controller to your pc, once connected the controller
will ~~~ vibrate ~~~~
```bash
sudo bash # root privileges
ros_load # alias to load env
rosrun ps3joy ps3joy_node.py
```

Now, this is the time to bringup turtlebot!
```bash
ros_load # alias to load env
roslaunch turtlebot_bringup minimal.launch
```

Yeah, now the L1 (boost mode), and L2 will be the deadman switch. The left joystick will be able
to control the moving of the turtlebot.

## Run Rtabmap with 3D camera

Run camera (Asus Xtion)
```bash
roslaunch openni2_launch openni2.launch
```

Another terminal
```bash
roslaunch rtabmap_tools mapping.launch
```

Now you can map your environment!

Once completed, save the 3D map pointcloud with command: 
`rosrun pcl_ros pointcloud_to_pcd input:=/rtabmap/scan_map`
