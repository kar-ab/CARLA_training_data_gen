# carla_data_gen


## Project description

This project is intended to generate training data for Autonomous Driving reserach using open source simulator i.e. Carla Simulator. 
In this project, an ego vehicle (vehicle.audi.tt) and other actors (vehicles / walking persons) are added to the simualtion. Sensors are attached to the ego vehicle and as the ego vehicle travels around in the environment, data from sensors are synchronously saved in respective folders. 
    
Following are the highlights of this project: 
    
1. Attach sensors easily using a yaml file: 
    Sensor Attributes for different sensor can be found [here](https://carla.readthedocs.io/en/0.9.9/ref_sensors/)
    Sample yaml files are provided for reference: 
    
    a. [stereo_vision.yaml](../blob/main/stereo_vision.yaml) 
        
    Two cameras, i.e. left and right are attached to vehicle. At the same position semantic segmentation and depth cameras are also attached to generate ground truth data for training. A sample of sensor data can be viewed [here](..blob/main/episodes/2021-05-14_00-06-47)
        
    b. [sensors.yaml](../blob/main/sensors.yaml)
    
    All types of sensor which can be attached to a vehicle in a Carla Simulator. A sample of sensor data can be viewed [here](..blob/main/episodes/2021-05-14_00-08-23)
    
3. Gather and save data synchronously from sensors and then the ego vehicle proceeds to next waypoint
4. By default, Ego vehicle movements are generated using the [BehaviorAgent](../blob/main/configure_agents/navigation/behavior_agent.py).
5. The same repository can be modified to work in online mode also, by just tweaking the Motion planning and Vehicle Control logic as per the incoming sensor data. 

## Setup:

1. Install [Carla Simulator](https://carla.org/2020/04/22/release-0.9.9/) .This work has been implemented on Carla v0.9.9 .
2. `git clone https://github.com/kar-ab/carla_data_gen`
3. Run script record_sync_data.py with the respective yaml file

    `$ python3 record_data_sync.py --yaml=sensors.yaml`  OR `$ python3 record_data_sync.py --yaml=stereo_vision.yaml`


## TODO list

0. Test for Semantic lidar data
1. Initial 10-15 seconds are taken for ego vehicle to generate vehicle control actions. possible solution - Maybe initial frames are being used to plan the vehicle path, need to start only sync only when vehicle has moved form its original location. 
2. Extract 2D and 3D bounding boxes for respective cameras
3. Integrating openscenario to add scenarios
4. Convert sensor data in KITTI / Cityscapes dataset format
5. Add measurements section for each frame: 
    location, accelerometer, compass, collision, theta, speed, target_speed, x_command, y_command, steer, throtthle , brake, gyroscope, GNSS, town
6. Provide a summary of data collected
7. For any RGB camera added: by default save 2D/3D boudning boxes, sem_seg info and depth camera details
8. Similarly: For any lidar added, save its semantic information
9. Create bounding boxes in lidar point cloud data automatically using transformations
## Credits: 

[Carla Simulator Team](https://carla.org/)
