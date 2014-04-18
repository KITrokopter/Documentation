Starting the crazyflie
----------------------
1. Plug in the crazyradios. You may attach more than one crazyradio at one PC - but then you have to set the dongle id manually when starting the quadcopter module.
2. Start the quadcopter modules. One for each crazyflie you want to fly.
3. The quadcopter modules announce themself at the API and get their ID.
4. Start the crazyflies. They should have the same orientation in order to have a unified yaw system.
5. When clicking "Scan for quadcopters" in the GUI the quadcopter module with the lowest id scans for available crazyflies.
6. The API distributes the quadcopter channel to the quadcopter modules.
7. Now you can check the distribution with the blink service.
8. Set the quadcopters tracking colors in the GUI