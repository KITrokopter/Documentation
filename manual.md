### Hardware

* Start all computers.
* Connect the Kinect. At most one Kinect per computer.
* Place the cameras as high angled as possible with best more than 25 degrees between two camera line of sights. You should choose one main camera that is in the middle of the three cameras.
* Connect the Crazyradios. (TODO: Maximum amount per computer?)
* On every computer, on every terminal you use for rosrun, execute `export ROS_IP=<ip of your machine>`.
* On every (! even the computer that will have roscore running) computer, on every terminal you use for rosrun, execute `export ROS_MASTER_URI=http://<ip of the machine that will run roscore>:11311`.
* Execute roscore on the machine set as ROS_MASTER_URI.

### Time synchronisation

The setup should have one central NTP server, and the other servers should only use this server.

To achieve this, you have to edit the files `/etc/ntp.conf` and `/etc/default/ntpdate`, if they exist.

* For the NTP server, just keep the entries, you don't have to change anything.
* For the clients, remove all other servers from the files and only add the ip of the one server on the local network.

Now, the servers should synchronize themselves within minutes after system startup.

You can check how good the synchronization is by running `sudo ntpdate -dvup 8 <ip>`. If the command fails, the main server is not yet synced.

### System

First Start:

 1. Open `~/ros_ws/src/api_application/API.cpp` and search the method `dummyFormation()` (Line 19). For each quadcopter that should be started, an entry in the vector has to be created. Simply copy the lines with the call to `push_back()` to achieve this. Edit the number in the return line to contain the number of starting quadcopters: `return APIFormation(positions, <number of starting quadcopters>)`.
 2. Start the GUI on any machine you want using `rosrun gui_application kitrokopter`.
 3. Starting cameras: First start main camera with `rosrun camera_application camera_application_node`. Then start camera of each other server with `rosrun camera_application camera_application_node`, note down the order of starting the camera_application_nodes for later (server 0, server 1, server 2,...). Starting was successfull if you get "Received images. Kinect seems to be working now.". Otherwise you should restart all camera after restarting the GUI (probably each camera has this bug at the first start).
 4. Execute `rosrun control_application control_application_node`.
 5. Enter chessboard values and press `Calibrate Cameras...`.
 6. Press `Start Calibration`.
 7. Press `Take Picture`, calibrate each camera alone (20-30 pictures) holding the chessboard right in front of the camera and later on take 15-30 pictures of each pair main camera and camera i. Be careful that the chessboard isn't moved during taking pictures as the cameras are not hardware synchronised with the others! Move the chessboard as close as possible in front of the camera. All corners on the chessboard have to be on the image.
 8. Press `Calculate Calibration`. If you plan to reuse the calibration, you should backup tmp/calibrationImages and tmp/calibrationResults.
 9. Start the quadcopter application on every machine that has a Crazyradio plugged in: `rosrun quadcopter_application crazyflie_node`
 10. Switch on the quadcopters that should start.
 11. Press `Scan for Quadcopters`. After this step no other quadcopter can be added. Adding a new quadcopter is only possible through restarting the GUI from now on.
 12. Double click on each Quadcopter and choose the color range min and max (for example pink is min: 324, 120, 100; max: 356, 120, 100). You can find the quadcopter through pressing `blink`. You can have a look in src/camera_application/images/colors.txt for the ranges. You should multiplicate H by 2.
 13. Press `Start System`. The quadcopters should start as soon as they are tracked. If you have to restart a quadcopter, you have to restart the GUI.


Restart of GUI/New Flight:

 1. Open `~/ros_ws/src/api_application/API.cpp` and search the method `dummyFormation()` (Line 19). For each quadcopter that should be started, an entry in the vector has to be created. Simply copy the lines with the call to `push_back()` to achieve this. Edit the number in the return line to contain the number of starting quadcopters: `return APIFormation(positions, <number of starting quadcopters>)`.
 2. Start the GUI on any machine you want using `rosrun gui_application kitrokopter`.
 3. Restart camera_application in the SAME order!
 4. Enter chessboard values and press `Calibrate Cameras...`.
 5. Press `Calculate Calibration`.
 6. Press on each camera picture to activate picture sending of the kinects.
 7. Start the quadcopter application on every machine that has a Crazyradio plugged in: `rosrun quadcopter_application crazyflie_node`
 8. Switch on the quadcopters that should start.
 9. Press `Scan for Quadcopters`. After this step no other quadcopter can be added. Adding a new quadcopter is only possible through restarting the GUI from now on.
 10. Double click on each Quadcopter and choose the color range min and max (for example pink is min: 324, 120, 100; max: 356, 120, 100). You can find the quadcopter through pressing `blink`. You can have a look in src/camera_application/images/colors.txt for the ranges. You must multiplicate H by 2.
 11. Press `Start System`. The quadcopters should start as soon as they are tracked. If you have to restart a quadcopter, you have to restart the GUI.

