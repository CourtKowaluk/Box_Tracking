# Box_Tracking
#
#
Before you start tracking a box, make sure that you have Motive using Optitrack installed and working. 

Setup:
In this case, the Motive streaming settings are as follows:
  
    Optitrack Streaming Engine
      Broadcast Frame: On
      Local Interface: loopback
      Labeled Markers: Off
      Unlabeled Markers: Off
      Asset Markers: Off
      Rigid Bodies: On
      Up Axis: Y Up
      Remote Trigger: Off
      Transmission Type: Multicast
      Command Port: 1510
      Data Port: 1511
      Multicast Interface: 239.255.42.99
      Multicast as Broadcast: On

Before you move and control a box, make sure you create the cube in the scene.
	Example:
  
    mosquitto_pub -h oz.andrew.cmu.edu -t realm/s/northstar/cube_t -m '{"object_id" : "cube_t", "action": "create", "type": "object", "data": {"object_type": "cube", "position": {"x": 0, "y": 0, "z": 0}, "rotation": {"x": 0, "y": 0, "z": 0, "w": 1}, "scale": {"x": 0.165, "y": 0.12, "z": 0.155}, "color": "#FF0000"}}' -r

The initial position doesn't matter. Make sure you use the '-r' flag to ensure the cube gets retained.

If you're tracking just a box, use the 'box_only_tracking' files. If you're also tracking a headset, use 'box_and_headset_tracking'. 
Make sure that the Streaming ID number in Motive for each rigid body matches up with the 'if(id==#)' in PythonCSample.py. For example, the Northstar Headset Streaming ID is 1, and the box is 2. 
If you add any more rigid bodies to track, make sure you update the id, pubtopic, and name in PythonSample.py, as well as updating the rate limiting with the TARGET_SEND_INTERVAL_ms variable in udp_relay.c. 

Run the udp_relay in a terminal (on Windows, use WSL), and use VisualStudio to run the PythonClient.
