Hardware setup:

 1. Place the cameras as high angled as possible with best more than 25 degrees between two camera line of sights. You should choose one main camera that is in the middle of the three cameras.
 2. Plug the cameras in the computers, at most one camera per computer.

First Calibration:

 1. Execute `roscore`.
 2. Synchronize times between servers.
 3. Open `~/ros_ws/src/api_application/API.cpp` and search the method `dummyFormation()` (Line 19). For each quadcopter that should be started, an entry in the vector has to be created. Simply copy the lines with the call to `push_back()` to achieve this. Edit the number in the return line to contain the number of starting quadcopters: `APIFormation(positions, <number of starting quadcopters>)`.
 4. Starting API: `rosrun api_application api_application_node`
 5. Starting cameras: First start main camera with `rosrun camera_application camera_application_node`. Then start camera of each other server with `rosrun camera_application camera_application_node`, note down the order of starting the camera_application_nodes for later (server 0, server 1, server 2,...). Starting was successfull if you get "Received images. Kinect seems to be working now.". Otherwise you should restart all camera after restarting the GUI (probably each camera has this bug at the first start).
 6. `rosrun control_application control_application_node`
 7. Starting new calibration: ros_ws/src/control_application/test/test-messages/start_calibration.sh IMPORTANT: This will delete all results of an old calibration!
 8. Take calibration pictures, starting with 15-30 pictures for each camera alone, later on take 15-20 pictures of each pair main camera and camera i: ros_ws/src/control_application/test/test-messages/take_calibration_pictures.sh
 9. calculating calibration with amcc toolbox: ros_ws/src/control_application/test/test-messages/calculate_calibration.sh. Note that pictures are saved in /tmp/calibrationImages/, output of calibration is saved in /tmp/calibrationResult/ important is stereo_calibration_i_0.mat. If you have problems with amcc toolbox calibration, you can check the log of matlab in /tmp/calibrationImages/log.
 10. insert IDs of all cameras: ros_ws/src/camera_application/test/test-messages/initialize_camera_id_n_color_green.sh <cameraId> or choose an other color.
 11. start tracking: ros_ws/src/control_application/test/test-messages/system_start.sh


Recalibration (restart of control_application_node):
	
 1. activate kinects: ros_ws/src/camera_application/test/test-messages/activate_picture_sending 
 2. calculating calibration with amcc toolbox: ros_ws/src/control_application/test/test-messages/calculate_calibration.sh.
 3. start tracking: ros_ws/src/control_application/test/test-messages/system_start.sh


Restart of camera_application:
	
 1. restart camera_application in the SAME order!
 2. activate kinects: ros_ws/src/camera_application/test/test-messages/activate_picture_sending 
 3. insert IDs of all cameras: ros_ws/src/camera_application/test/test-messages/initialize_camera_id_n_color_green.sh <cameraId> or choose an other color.
 4. calculating calibration with amcc toolbox: ros_ws/src/control_application/test/test-messages/calculate_calibration.sh.
 5. start tracking: ros_ws/src/control_application/test/test-messages/system_start.sh
