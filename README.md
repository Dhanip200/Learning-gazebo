# Learning-gazebo
Hi I am Dhanip Modi an Aspiring robotics and AI enginner i am learning how to use ros and gazebo. This is muy attemp in learning gazebo and ros
I launched WSl and in that installed gazebo (currently running on docker).
✅ 3 Working Options for You:
🟢 Option 1: Use Docker (Recommended)
If you just want to run Gazebo, Docker is the cleanest and most stable method on Noble.

Downlode the Docker in wsl(I am using ros-jazzy,ubuntu24.04,gazebo harmonic).
1. Prepare Docker in WSL
First, make sure you have Docker installed and running inside your WSL Ubuntu 24.04.

If you haven't installed Docker yet:
bash
Copy
Edit
sudo apt update
sudo apt install docker.io
sudo service docker start
sudo usermod -aG docker $USER
After this, exit WSL and reopen so that your user is in the docker group.

Test Docker:

bash
Copy
Edit
docker run hello-world
