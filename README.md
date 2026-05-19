# Foxy_sensor_drivers
- This repo includes
  - Witmotion IMU
  - Realsense
  - Veodyne

## Requirements
  ```bash
  sudo apt-get install libqt5serialport5-dev
  ```
  - Realsense driver
  ```bash
  sudo apt install ros-foxy-realsense2-*
  ```
  - otherwise,
    ```bash
    sudo mkdir -p /etc/apt/keyrings
    curl -sSf https://librealsense.realsenseai.com/Debian/librealsenseai.asc | \
    gpg --dearmor | sudo tee /etc/apt/keyrings/librealsenseai.gpg > /dev/null
    
    echo "deb [signed-by=/etc/apt/keyrings/librealsenseai.gpg] https://librealsense.realsenseai.com/Debian/apt-repo `lsb_release -cs` main" | \
    sudo tee /etc/apt/sources.list.d/librealsense.list
    sudo apt-get update

    sudo apt-get install librealsense2-dkms librealsense2-utils librealsense2-dev librealsense2-dbg

    sudo apt install ros-foxy-realsense2-*
    ```

## Run
ros2 param list
- Realsense
  ```bash
  ros2 launch realsense2_camera rs_launch.py \
    rgb_camera.profile:=640x480x30 \
    depth_module.profile:=640x480x30 \
    enable_sync:=true \
    align_depth.enable:=true
  ```
- Velodyne
  - Set IP as 192.168.1.100
  - If some issue occurs, use wireshark to find IP address
    ```bash
    sudo apt install wireshark
    sudo wireshark
    ```
  ```bash
  ros2 launch velodyne velodyne-all-nodes-VLP32C-launch.py
  ```

- IMU
  ```bash
  sudo chmod a+w+r+x /dev/ttyUSB0
  ros2 launch witmotion_ros wt901.launch.py
  ```