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
  * Move the chessboard as close as possible in front of the camera. All corners on the chessboard have to be on the image. Try to hold the chessboard for one or two pictures in the corners of the camera image. Otherwise, the image might be strangely distorted after calibration.
* Start the control application.
* Calibrate the camera system.
  * First, make 5 pictures for every camera, holding the chessboard right in front of the camera.
  * Then, make pairwise pictures for cameras (0, 1) and (0, 2). About 15 per pair should be enough.
* Start the quadcopter application on every machine that has a Crazyradio plugged in.
* !!! TODO: insert information about quadcopter id mapping.
