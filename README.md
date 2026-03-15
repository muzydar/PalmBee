## PalmBee

PalmBee is a package designed to automate the pollination process in palm tree plantations using drones. This package leverages the capabilities of PX4 and ROS2 Humble to provide an efficient and reliable solution for pollination.

## Compatibility

- **Ubuntu 22.04**
- **ROS2 Humble**
- **ZED SDK 4.2 ( with ZED Wrapper 4.2.5 )**
- **Ardupilot**
- **Jetpack 6.2.x**

## Installation

To install the PalmBee package, follow these steps:

1. Install and setup ROS2 Humble First:
    ```bash
    using this documentation
    https://docs.ros.org/en/humble/Installation.html
    ```

2. Install and setup this specific Zed SDK:
    ```bash
    [git clone https://github.com/ep51lon/PalmBee.git](https://www.stereolabs.com/en-id/developers/release/4.2
    note : this repository is based on wrapper 4.2.5 and tested on ZED SDK for JetPack 6.1 and 6.2 (L4T 36.4))
    ```

3. Create the workspace directory:
    ```bash
    mkdir -p palmbee_ws/src
    cd palmbee_ws/src
    ```

5. Clone the repository:
    ```bash
    git clone https://github.com/ep51lon/PalmBee.git
    ```

4. Install dependencies:
    ```bash
    git clone https://github.com/ep51lon/PalmBee.git
    ```
    or build specific package (for example, pb_perception) using
    ```bash
    colcon build --packages-select pb_perception
    ```

5. Build the package:
    ```bash
    colcon build
    or build specific package (for example, pb_perception) using
    colcon build --packages-select pb_perception
    ```

5. Source the setup file:
    ```bash
    source install/setup.bash
    ```
    or set it up on ~/.bashrc using the source command
    ```bash
    note : for yolo_ws / u can also build it on different workspace and build it too ( but u must install / set yolo first and any package that yolo needed )
    ```

## Usage

**TODO**

To use the PalmBee package, follow these steps:

1. Launch camera (for example using Realsense):
    ```bash
    ros2 launch pb_perception rs_slam_launch.py
    ```

2. Launch AprilTag Detector:
    ```bash
    ros2 launch pb_perception rs_apriltag_launch.py
    ```

3. Get annotated image and coordinates:
    ```bash
    ros2 run pb_perception get_markers.py
    ```

4. Open your favorite image viewer to display the anotated image:
    ```bash
    ros2 run rqt_image_view rqt_image_view
    ```
    and select the image topic to display.

**TO START AUTOMATION**

1. run or start stack script

Stack script are a .sh type file that are there so it's make the starting or running the ROS2 package much more easier since for this repository, it needed to run more or less 6 package ( included rosbag for logging purpose )
Stack script for this purpose located in ~/script/ with file name start_pb_stack.sh. to start it, because it's a normal script, no need to build it, just chmod +x "path of the file" to make it executable.
example :
```bash
chmod +x ~/script/start_pb_stack.sh
~/script/start_pb_stack.sh
```
note :
wait until all the terminal ros2 package windows to finish starting and the stack script done running, don't forget to check mission planner for bad vision warning !

2. starting yolo package

the yolo ros2 executable for object detection are located in ~/yolo_ws/src/yolov11_ros/yolov11_ros/yolo_node.py , after colcon build it, to start the executable here the command for it :
```bash
ros2 launch yolob11_ros yolo_v11_ros_launch.py
```

wait until there's nomore new line being shown in the terminal or the coordinate of the detected object to be shown in terminal ( if the object are possible to be detected in ground ). if yolo still can't detected the desirable object in ground, this yolo package still can detect and send the desirable object coordinat when the vehicle or drone move / fly.
note : becareful when it's only posible to detect the object after the vehicle starting / moving, since yolo keep sending coordinate of it's desirable detected object 

3. starting control manager package

Control manager package are there to command the vehicle or drone to move depend's on what being commanded ( for this case, it's a circular motion after take off and object detected with it's coordinate ), this package is usually located in the same workspace as the main palmbee_ws ( in ~/palmbee_ws/src/PalmBee/pb_control/src/cm_setpoint.cpp ). to start this package, use this command :
```bash
ros2 launch pb_control  cm_setpoint.launch.py
```
note : there's one more executable from pb_control that can be used if needed 2 different kind of executable.

after starting , wait until in the terminal where this package startet to show "waiting for arm". to armed the vehicle, use mission planner or GCS to do it. after the drone being armed by GCS, it will start flying automaticly according to it's mission 

For more detailed instructions and documentation, please refer to the [wiki](https://github.com/yourusername/palmbee/wiki).

## Contributing

We welcome contributions to the PalmBee package. Please fork the repository and submit pull requests for any enhancements or bug fixes.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
