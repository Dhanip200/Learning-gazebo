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
gz sim
'''
(if not running try using wifi ip--1st do this export DISPLAY=$(grep nameserver /etc/resolv.conf | awk '{print $2}'):0and then this-- export DISPLAY=//192.168.1.164:0//)
