##  Desctiption package
    This package is made on the RB-1 robot https://robotnik.eu/es/productos/robots-moviles/rb-1-base/, it provides all the urdf files and xacro files that describe the robot, controllers and launch files for the gazebo simulation of the RB-1 robot, the controllers loaded in the launch file are joint_state_broadcaster and diff_drive_controller so the robot can be controlled with speed commands. 

    It will also be possible to load the controller for the platform, we leave this up to the user.
    
    All steps for launching the simulation, controlling the robot speed and activating the platform controller are described below.

##  Installation instructions
    The following steps are for installing the "rb1_ros2_description" package in a workspace.
            - STEP1: Go to your ros2/src workspace, for this example we will consider that your workspace is called "ros2_ws" and that it is located in your user directory

                    command:            cd ~/ros2_ws/src

            - STEP2: Clone the github package

                    command:            git clone -r https://github.com/morg1207/checkpoint8.git

            - STEP3: Build package
                    command:            cd ~/ros2_ws
                                        colcon build 
                                        source ~/ros2_ws/install/setup.bash

##  Getting started
    The following steps are for activating the simulation
            - STEP 1: Execute the following command

                    command:            ros2 launch rb1_ros2_description rb1_ros2_xacro.launch.py     

    Note: The simulation takes about 1 min to start, so wait for it to start.

##  Controller activation
    The following steps must be followed to activate the controller for elevator:
            -STEP 1 : Execute the following command
            
                    command :            ros2 control load_controller --set-state start elevator_effort_controller

                     output successful: Sucessfully loaded controller elevator_effort_controller into state active


##  Moving the robot's lifting unit
    To move the litting unit, it must be published in the topic "/elevator_effort_controller/commands" as follows:
            - to lift the platform

                    command :            ros2 topic pub /elevator_effort_controller/commands  std_msgs/msg/Float64MultiArray "{data: [10.0]}" -1

            - to lower the platform

                    command :            ros2 topic pub /elevator_effort_controller/commands  std_msgs/msg/Float64MultiArray "{data: [0.0]}" -1

## Send speed commands to the robot

            command:    ros2 topic pub --rate 10 /rb1_base_controller/cmd_vel_unstamped geometry_msgs/msg/Twist "{linear: {x: 0.0, y: 0, z: 0.0}, angular: {x: 0.0,y: 0.0, z: 0.2}}"
