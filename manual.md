Hardware setup:

 1. Place the cameras as high angled as possible.
 1.1. The angle between two camera line of sights should be at least 25 degrees.
 2. Plug the cameras in the computers, at most one camera per computer.


First Start:

 1. Execute `roscore`.
 2. Synchronize times between servers. Have a look at ntp.md.
 3. Starting GUI: `rosrun gui_application kitrokopter`.
 4. Starting cameras: For each server that has a camera plugged in: `rosrun camera_application camera_application_node`, note down the order of starting the camera_application_nodes for later (0, 1, 2,...). Starting was successfull if you get "Received images. Kinect seems to be working now.". Otherwise you should restart all cameras after restarting the GUI.
 5. Execute `rosrun control_application control_application_node`.
 6. Press `Calibrate Cameras...`.
 7. Press `Start Calibration`.
 8. Press Take Picture, calibrate each camera alone (10-20 pictures) and later on take 15-30 pictures of each pair camera 0 and camera i.
 9. Press `Calculate Calibration`.
 10. Starting Quadcopter: `rosrun quadcopter_application crazyflie_node`
 11. Press `Scan for Quadcopters`.
 12. Double click on each Quadcopter and choose the color range min and max (for example pink is min: 324, 120, 100; max: 356, 120, 100)
 13. Press `Start System`.


Restart of GUI/New Flight:
	
 1. Starting GUI: `rosrun gui_application kitrokopter`
 2. Restart camera_application in the SAME order!
 3. Press `Calibrate Cameras...`.
 4. Press `Calculate Calibration`.
 5. Press on each camera picture to activate picture sending.
 6. Starting Quadcopter: `rosrun quadcopter_application crazyflie_node`
 7. Press `Scan for Quadcopters`.
 8. Double click on each Quadcopter and choose the color range min and max (for example pink is min: 324, 120, 100; max: 356, 120, 100)
 9. Press `Start System`.
