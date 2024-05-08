Here's the revised version of your guide in markdown format, suitable for inclusion in a README file. I have corrected syntax errors and clarified some steps to make them more user-friendly.
Guide on How to Get Data from OptiTrack into ROS

This guide explains how to publish data from the OptiTrack system to a ROS core. The OptiTrack System utilizes Motive Software to interpret the data.
1. Log into the Robotics Lab Server

If you are in the Robotics Lab, log into Hydra using your username and password:

```bash

ssh username@hydra
```
2. Install the VRPN Package

You need to install the VRPN package into the ROS environment. Run the following command in your terminal:

```bash

sudo apt install ros-$(rosversion -d)-vrpn-client-ros
```
3. Create a Catkin Package

Create a Catkin package named optitrack_ros_client. Replace <dependencies> with any additional dependencies your project might require:

```bash

catkin_create_pkg optitrack_ros_client std_msgs rospy roscpp <dependencies>
```
4. Create a Launch Folder and File

Create a launch folder in your package directory, and then create a launch file inside this folder. You can use your favorite text editor to create the file named optitrack.launch.

Here's an example of what you might include in optitrack.launch. Remember, the IP address should be that of the computer running the Motive Software:

```xml

<launch>
  <node name="vrpn_client_node" pkg="vrpn_client_ros" type="vrpn_client_node" output="screen">
    <param name="server" value="YOUR_MOTIVE_COMPUTER_IP"/>
    <param name="frame_id" value="world"/>
    <!-- List your tracked objects here -->
    <param name="tracked_objects" type="string" value="Object1, Object2"/>
  </node>
</launch>
```

5. Launch the Node

Run the following command to start the node and begin receiving data from OptiTrack:

```bash

roslaunch optitrack_ros_client optitrack.launch
```
This setup should help you integrate OptiTrack data into your ROS environment efficiently. Ensure that you replace placeholders like YOUR_MOTIVE_COMPUTER_IP and <dependencies> with actual values based on your setup and requirements.