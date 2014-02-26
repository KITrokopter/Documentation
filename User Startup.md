Starting the system as seen by the user
---------------------------------------

### ROS

* Start all computers.
* Connect the Kinect. At most one Kinect per computer.
* Connect the Crazyradios. (TODO: Maximum amount per computer?)
* On every computer, on every terminal you use for rosrun, execute `export ROS_IP=<ip of your machine>`.
* On every (! even the computer that will have roscore running) computer, on every terminal you use for rosrun, execute `export ROS_MASTER_URI=http://<ip of the machine that will run roscore>:11311`.
* Execute roscore on the machine set as ROS_MASTER_URI.

### KITrokopter

* Start the API on any machine you want.
* Start the camera application on every machine that has a Kinect plugged in.
* Calibrate the cameras.
* Start the control application.
* Calibrate the camera system.
* Start the quadcopter application on every machine that has a Crazyradio plugged in.
* !!! TODO: insert information about quadcopter id mapping.
