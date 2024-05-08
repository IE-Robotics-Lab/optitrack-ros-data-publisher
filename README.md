# OptiTrack to ROS
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

Create a launch folder in your package directory, and then create a launch file inside this folder. 

Here's an example of what you might include in [optitrack.launch](optitrack.launch). Remember, the IP address should be that of the computer running the Motive Software:

```xml

<launch>

  <arg name="server" default="10.205.3.3"/>

  <node pkg="vrpn_client_ros" type="vrpn_client_node" name="optitrack" output="screen">
    <rosparam subst_value="true">
      server: $(arg server)
      port: 3883

      update_frequency: 120.0
      frame_id: world

      # Use the VRPN server's time, or the client's ROS time.
      use_server_time: false
      broadcast_tf: true

      # Must either specify refresh frequency > 0.0, or a list of trackers to create
      refresh_tracker_frequency: 1.0
      #trackers:
      #- FirstTracker
      #- SecondTracker
    </rosparam>
  </node>

</launch>

```

5. Launch the Node

Run the following command to start the node and begin receiving data from OptiTrack:

```bash

roslaunch optitrack_ros_client optitrack.launch
```
This setup should help you integrate OptiTrack data into your ROS environment efficiently. Ensure that you replace placeholders like YOUR_MOTIVE_COMPUTER_IP and <dependencies> with actual values based on your setup and requirements.
