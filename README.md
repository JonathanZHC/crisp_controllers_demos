# CRISP Controllers Demos

This is haocheng's personal version of repo "crisp_controllers_demos" (https://github.com/utiasDSL/crisp_controllers_demos).


# Option 1: clone Crisp_controllers_demos from my fork

## Clone the repo
```bash
git clone git@github.com:JonathanZHC/crisp_controllers_demos.git crisp_controllers_demos
cd crisp_controllers_demos
```

## Build the provided container
```bash
docker compose build
```

## Start the provided container
```bash
ROBOT_IP=172.16.0.2 FRANKA_FAKE_HARDWARE=true docker compose up launch_franka
```


# Option 2: alternatively, you can also clone Crisp_controllers_demos from LSY repo

## Clone the repo
```bash
git clone git@github.com:utiasDSL/crisp_controllers_demos.git crisp_controllers_demos
cd crisp_controllers_demos
git clone git@github.com:utiasDSL/crisp_controllers.git crisp_controllers
```

## Change some parameters
crisp_controllers_robot_demos/launch/franka.launch.py: line 200: "rate": change to 100
crisp_controllers_robot_demos/config/fr3/fr3.rviz: line 158: frame rate: change to 100
crisp_controllers_robot_demos/crisp_controllers_robot_demos/target_publisher.py: line 32: change to 100.0

## Ensure ROS_DOMAIN_ID in all Crisp_controllers_demos project to be 101
search for it and correct all of them

## Optionally, put the following lines after clone franka_ros2 shells in dockerfile if you want to use calibrated fr3 urdf model
```bash
RUN git clone https://github.com/JonathanZHC/kinematics_calibration.git /tmp/kin_calib \
    && mkdir -p src/franka_description/robots/fr3 \
    && cp /tmp/kin_calib/calibrated_urdf/fr3_1/kinematics.yaml \
          src/franka_description/robots/fr3/kinematics.yaml \
    && echo ">>> Replaced FR3 kinematics.yaml with calibrated version <<<" \
    && rm -rf /tmp/kin_calib
```

## Build the provided container
```bash
docker compose build
```

## Start the provided container
```bash
ROBOT_IP=172.16.0.2 FRANKA_FAKE_HARDWARE=true docker compose up launch_franka
```

