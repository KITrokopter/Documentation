camera position: as high-angled as possible

First Calibration:

	1. roscore
	2. starting API: catkin_make api_application_node && rosrun api_application api_application_node
	3. starting cameras: for each camera at an own server: catkin_make camera_application_node && rosrun camera_application camera_application_node, note order of starting camera_application_node for later (0, 1, 2,...). Starting was successfull if you get "Received images. Kinect seems to be working now.". Otherwise you should restart the camera.
	4. catkin_make control_application_node && rosrun control_application control_application_node
	5. starting new calibration: ros_ws/src/control_application/test/test-messages/start_calibration.sh IMPORTANT: This will delete all results of an old calibration!
	6. take calibration pictures, starting with 5-10 pictures for each camera alone, later on take 15-20 pictures of each pair camera 0 and camera i: ros_ws/src/control_application/test/test-messages/take_calibration_pictures.sh
	7. calculating calibration with amcc toolbox: ros_ws/src/control_application/test/test-messages/calculate_calibration.sh. Note that pictures are saved in /tmp/calibrationImages/, output of calibration is saved in /tmp/calibrationResult/ important is stereo_calibration_i_0.mat. If you have problems with amcc toolbox calibration, you can check the log of matlab in /tmp/calibrationImages/log
	(camera 0: 5 Bilder, camera 1: 5-10 Bilder, camera 2: 5-10 Bilder, cameras 0,1: (2-3)x5 Bilder, cameras 0,2: (2-3)x5 Bilder) 
	8. insert IDs of all cameras: ros_ws/src/camera_application/test/test-messages/initialize_camera_id_n_color_green.sh <cameraId>
	9. synchronize times between servers. Have a look at ntp.md.
	10. start tracking: ros_ws/src/control_application/test/test-messages/system_start.sh


Recalibration (restart of control_application_node):
	
	1. activate kinects: ros_ws/src/camera_application/test/test-messages/activate_picture_sending 
	2. calculating calibration with amcc toolbox: ros_ws/src/control_application/test/test-messages/calculate_calibration.sh.
	3. start tracking: ros_ws/src/control_application/test/test-messages/system_start.sh


Restart of camera_application:
	
	1. restart camera_application in the SAME order!
	2. activate kinects: ros_ws/src/camera_application/test/test-messages/activate_picture_sending 
	3. insert IDs of all cameras: ros_ws/src/camera_application/test/test-messages/initialize_camera_id_n_color_green.sh <cameraId>
	4. calculating calibration with amcc toolbox: ros_ws/src/control_application/test/test-messages/calculate_calibration.sh.
	5. start tracking: ros_ws/src/control_application/test/test-messages/system_start.sh
