# Intel-RealSense-SDK-and-ROS2-package-installation

Run the following terminal commands:

sudo apt update && sudo apt upgrade -y

sudo apt install git cmake build-essential libusb-1.0-0-dev pkg-config libgtk-3-dev -y

sudo apt install libglfw3-dev libgl1-mesa-dev libglu1-mesa-dev -y

cd ~

git clone https://github.com/IntelRealSense/librealsense.git

cd librealsense

mkdir build && cd build

cmake .. -DCMAKE_BUILD_TYPE=Release

make -j$(nproc)

sudo cp config/99-realsense-libusb.rules /etc/udev/rules.d/

sudo udevadm control --reload-rules && udevadm trigger

Ignore the errors and proceed to reboot

sudo reboot

Test the camera

realsense-viewer

You can list connected RealSense devices with:

rs-enumerate-devices

Follow these commands for ROS2 package installation:

cd to your ros2 workspace src folder (ros2_ws/src) and then:

git clone https://github.com/IntelRealSense/realsense-ros.git

sudo apt update

rosdep install --from-paths src --ignore-src -y

cd ~/ros2_ws

colcon build 

source ~/.bashrc

If you get errors during colcon build try to remove (rm -rf) your build, installation and log folder. Then run colcon build again.

Launch the RealSense camera node

ros2 launch realsense2_camera rs_launch.py

List available ros2 topics

ros2 topic list

Then you can use rviz to check out the camera feed!
