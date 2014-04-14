Hardware setup:

 1. Place the cameras as high angled as possible with best more than 25 degrees between two camera line of sights. You should choose one main camera that is in the middle of the three cameras.
 2. Plug the cameras in the computers, at most one camera per computer.


First Start:

 1. Execute `roscore`.
 2. Synchronize times between servers. Have a look at ntp.md.
 3. Open `~/ros_ws/src/api_application/API.cpp` and search the method `dummyFormation()` (Line 19). For each quadcopter that should be started, an entry in the vector has to be created. Simply copy the lines with the call to `push_back()` to achieve this. Edit the number in the return line to contain the number of starting quadcopters: `APIFormation(positions, <number of starting quadcopters>)`.
 4. Starting GUI: `rosrun gui_application kitrokopter`.
 5. Starting cameras: First start main camera with `rosrun camera_application camera_application_node`. Then start camera of each other server with `rosrun camera_application camera_application_node`, note down the order of starting the camera_application_nodes for later (server 0, server 1, server 2,...). Starting was successfull if you get "Received images. Kinect seems to be working now.". Otherwise you should restart all camera after restarting the GUI (probably each camera has this bug at the first start).
 6. Execute `rosrun control_application control_application_node`.
 7. Enter chessboard values and press `Calibrate Cameras...`.
 8. Press `Start Calibration`.
 9. Press Take Picture, calibrate each camera alone (10-30 pictures) and later on take 15-30 pictures of each pair main camera and camera i. Be careful that the chessboard isn't moved during taking pictures as the cameras are not hardware synchronised with the others!
 10. Press `Calculate Calibration`. If you plan to reuse the calibration, you should backup tmp/calibrationImages and tmp/calibrationResults.
 11. Starting Quadcopter: `rosrun quadcopter_application crazyflie_node`
 12. Switch on the quadcopters that should start.
 13. Press `Scan for Quadcopters`. After this step no other quadcopter can be added. Adding a new quadcopter is only possible through restarting the GUI from now on.
 14. Double click on each Quadcopter and choose the color range min and max (for example pink is min: 324, 120, 100; max: 356, 120, 100). You can find the quadcopter through pressing `blink`. You can have a look in src/camera_application/images/colors.txt for the ranges. You should multiplicate H by 2.
 15. Press `Start System`. The quadcopters should start as soon as they are tracked. If you have to restart a quadcopter, you have to restart the GUI.


Restart of GUI/New Flight:

 1. Open `~/ros_ws/src/api_application/API.cpp` and search the method `dummyFormation()` (Line 19). For each quadcopter that should be started, an entry in the vector has to be created. Simply copy the lines with the call to `push_back()` to achieve this. Edit the number in the return line to contain the number of starting quadcopters: `APIFormation(positions, <number of starting quadcopters>)`.
 2. Starting GUI: `rosrun gui_application kitrokopter`
 3. Restart camera_application in the SAME order!
 4. Enter chessboard values and press `Calibrate Cameras...`.
 5. Press `Calculate Calibration`.
 6. Press on each camera picture to activate picture sending of the kinects.
 7. Starting Quadcopter: `rosrun quadcopter_application crazyflie_node`
 8. Switch on the quadcopters that should start.
 9. Press `Scan for Quadcopters`. After this step no other quadcopter can be added. Adding a new quadcopter is only possible through restarting the GUI from now on.
 10. Double click on each Quadcopter and choose the color range min and max (for example pink is min: 324, 120, 100; max: 356, 120, 100). You can find the quadcopter through pressing `blink`. You can have a look in src/camera_application/images/colors.txt for the ranges. You should multiplicate H by 2.
 11. Press `Start System`. The quadcopters should start as soon as they are tracked. If you have to restart a quadcopter, you have to restart the GUI.

