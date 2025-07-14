# Learning-gazebo
Hi I am Dhanip Modi an Aspiring robotics and AI enginner i am learning how to use ros and gazebo. This is muy attemp in learning gazebo and ros
I launched WSl and in that installed gazebo (currently running on docker).
✅ 3 Working Options for You:
🟢 Option 1: Use Docker (Recommended)
If you just want to run Gazebo, Docker is the cleanest and most stable method on Noble.

Downlode the Docker in wsl(I am using ros-jazzy,ubuntu24.04,gazebo harmonic).

⚙️ 1. Set up your environment:
''' bash
sudo apt update && sudo apt upgrade -y
sudo apt install locales curl gnupg lsb-release -y
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
'''
2. Add the ROS 2 Jazzy repository
''' bash
sudo apt install software-properties-common
sudo add-apt-repository universe

sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] \
http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

sudo apt update
'''
3.Install ROS 2 Jazzy desktop:-
'''bash
sudo apt install ros-jazzy-desktop -y
'''

 4.Source ROS 2 setup:-
 '''bash
 echo "source /opt/ros/jazzy/setup.bash" >> ~/.bashrc
source ~/.bashrc
'''

5. Test ROS 2 works:-
'''bash
ros2 run demo_nodes_cpp talker
'''
open another terminal
'''ros2 run demo_nodes_cpp listener

 6. Install Gazebo Harmonic
:-
a. Add the Gazebo Harmonic repo:-
'''bash
sudo apt install curl gnupg2 lsb-release -y
sudo curl -sSL http://packages.osrfoundation.org/gazebo.key -o /usr/share/keyrings/gazebo-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/gazebo-archive-keyring.gpg] \
http://packages.osrfoundation.org/gazebo/ubuntu-stable $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/gazebo-stable.list > /dev/null

sudo apt update
'''
b. Install Harmonic
'''bash
sudo apt install gz-harmonic -y
'''
You can run it using:
'''bash

use nano Dockerfile (delet everything) and print
'''bash 
# Use Ubuntu 24.04 base image
FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive

# Setup locale
RUN apt-get update && apt-get install -y locales && \
    locale-gen en_US en_US.UTF-8 && update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8

# Install curl, gnupg, lsb-release, software-properties-common for repo setup
RUN apt-get update && apt-get install -y curl gnupg2 lsb-release software-properties-common

# Add ROS 2 apt repository
RUN curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add - && \
    echo "deb http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros2.list

# Install ROS 2 desktop, Gazebo ROS packages, and dependencies
RUN apt-get update && apt-get install -y \
    ros-jazzy-desktop \
    ros-jazzy-gazebo-ros-pkgs \
    python3-rosdep \
    python3-colcon-common-extensions \
    build-essential \
    cmake \
    git \
    python3-pip \
    sudo \
    wget

# Initialize rosdep
RUN rosdep init || true
RUN rosdep update

# Setup entrypoint to source ROS 2 environment automatically
SHELL ["/bin/bash", "-c"]
RUN echo "source /opt/ros/jazzy/setup.bash" >> ~/.bashrc

CMD ["/bin/bash"]

'''
Ctrl+0--> enter -->Ctrl+x

then run
'''bash
docker build -t ros2-jazzy-gazebo .
'''


gz sim
'''
(if not running try using wifi ip--1st do this export DISPLAY=$(grep nameserver /etc/resolv.conf | awk '{print $2}'):0and then this-- export DISPLAY=//192.168.1.164:0//)
print this:-
'''bash
docker run -it --rm \
  -e DISPLAY=$DISPLAY \
  -e QT_X11_NO_MITSHM=1 \
  -v /tmp/.X11-unix:/tmp/.X11-unix:rw \
  osrf/ros:humble-desktop
  '''

then run sudo
'''bash
sudo apt update
sudo apt search ros-noble-gazebo-ros-pkgs
sudo apt search ros-jazzy-gazebo-ros-pkgs
'''


this for launching turtle bot
'''bash
# 1. Install turtlebot3 simulation and dependencies
apt update
apt install -y ros-humble-turtlebot3-gazebo ros-humble-turtlebot3-msgs

# 2. Set required environment variable
echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc
export TURTLEBOT3_MODEL=burger

# 3. Source ROS
source /opt/ros/humble/setup.bash

# 4. Try launching again
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
...
---------------------------------------------------------
to get in docker(in another wsl terminal)
'''bash
docker run -it --rm \
  -e DISPLAY=$DISPLAY \
  -e QT_X11_NO_MITSHM=1 \
  -v /tmp/.X11-unix:/tmp/.X11-unix:rw \
  osrf/ros:humble-desktop
'''
----------------------------------------------------------
use this to launch the bot
'''bash
       source /opt/ros/humble/setup.bash
       ros2 run teleop_twist_keyboard teleop_twist_keyboard
'''

ADDING A Python File:-
'''bash
mkdir -p ~/ros2_ws/src/my_bot_controller/my_bot_controller
cd ~/ros2_ws/src/my_bot_controller/my_bot_controller

nano move_bot.py
'''

 Step 1: Create the destination path inside the container
 '''bash
 docker exec -it silly_turing mkdir -p /root/ros2_ws/src/my_bot_controller/my_bot_controller
'''
Step 2: Copy the file into the container
'''bash
docker cp ~/ros2_ws/src/my_bot_controller/my_bot_controller/move_bot.py silly_turing:/root/ros2_ws/src/my_bot_controller/my_bot_controller/
'''

go into the docker file :-
'''bash
docker exec -it silly_turing bash
'''

inside container go to this file:-
'''bash
cd /root/ros2_ws/src/my_bot_controller
 '''

 -->making a file
 '''bash
 touch setup.py
 '''

 ---> gettinginto the file(1st install nano with this :-apt update
apt install nano):-
'''bash
 nano setup.py
 '''
 paste this :-
 '''
 # setup.py
from setuptools import setup

package_name = 'my_bot_controller'

setup(
    name=package_name,
    version='0.0.0',
    packages=[package_name],
    install_requires=['setuptools'],
    zip_safe=True,
    maintainer='your_name',
    maintainer_email='your_email@example.com',
    description='Simple bot controller',
    license='Apache License 2.0',
    tests_require=['pytest'],
    entry_points={
        'console_scripts': [
            'move_bot = my_bot_controller.move_bot:main',
        ],
    },
)
'''

create this file:-
'''bash
touch package.xml
nano package.xml
'''
paste this:-'''
<?xml version="1.0"?>
<package format="3">
  <name>my_bot_controller</name>
  <version>0.0.0</version>
  <description>My TurtleBot3 Controller</description>
  <maintainer email="you@example.com">Your Name</maintainer>
  <license>Apache-2.0</license>

  <buildtool_depend>ament_cmake</buildtool_depend>
  <buildtool_depend>ament_python</buildtool_depend>

  <exec_depend>rclpy</exec_depend>
  <exec_depend>geometry_msgs</exec_depend>

  <build_type>ament_python</build_type>
</package>
'''
2. Build the workspace
From inside the container:

'''bash
cd /root/ros2_ws
colcon build
'''

Then source the environment:

'''bash

source install/setup.bash
'''
3. Run the node
If your node script is correct (with main() function and publisher logic), run:

'''bash
ros2 run my_bot_controller move_bot
'''
----------------------------------------------------------------------------------------------------------------------python package publishing-------------------------------------------------------------------------------------------------------------------------------
Installing colcon:-
'''bash
sudo apt install python3-colcon-common-extensions
'''

Navigating to our folder:-
'''bash
cd ~/ros2_ws/src
'''

Creating Commonds:-
'''bash
ros2 pkg create --build-type ament_python py_pubsub
'''

Making publisher and subscriber files inside py_pubsub inside py_pubsub:-
'''bash
cd ~/ros2_ws/src/py_pubsub/py_pubsub
touch publisher_member_function.py subscriber_member_function.py
'''
