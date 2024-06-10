Hello, welcome to my little project! Yes, I'm using a template from a content creator who really helped me get started with ROS.

This project is meant to run on Ubuntu 23.04 (Lunar Lobster).

Because I've followed a tutorial and I have no idea on how do it on my own, we will use docke to work in a ubuntu 22.04 environment on our ubuntu 23.04 host.

### Step-by-Step Setup Instructions

### STEP 1: Install Docker and Set Up a Container
Yes, you're on the right track. Using Docker is a great solution for running software that requires a specific operating system version or environment. Here's a step-by-step guide to help you set this up:

1. **Install Docker on Ubuntu 23.04**:
   ```bash
   sudo apt update
   sudo apt install docker.io
   sudo systemctl start docker
   sudo systemctl enable docker
   ```

2. **Create a Docker Container with Ubuntu 22.04**:
   You can create a Docker container that runs Ubuntu 22.04.

   ```bash
   sudo docker pull ubuntu:22.04
   sudo docker run -it ubuntu:22.04 /bin/bash
   ```

   This command will pull the Ubuntu 22.04 image from Docker Hub and start a new container with an interactive terminal.

3. **Set Up the Container for ROS Humble**:
   Inside the container, you'll need to set up ROS Humble and any other dependencies as per your tutorial.

   ```bash
   apt update

   apt install -y locales

   locale-gen en_US en_US.UTF-8

   update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
   apt install -y software-properties-common
   add-apt-repository universe
   apt update
   apt install -y curl gnupg2 lsb-release

   curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add -
   sh -c 'echo "deb http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros2-latest.list'

   echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | tee /etc/apt/sources.list.d/ros2.list > /dev/null

   apt update

   sudo apt upgrade

   apt install -y ros-humble-desktop
   ```
4. **Sourcing the setup script**:
Replace ".bash" with your shell if you're not using bash
Possible values are: setup.bash, setup.sh, setup.zsh
    ```bash
    source /opt/ros/humble/setup.bash
    ```
4. **Testing to see if it works**:
open a new terminal (see section bellow)
in the first terminal type
    ```bash
    source /opt/ros/humble/setup.bash
    ros2 run demo_nodes_cpp talker
    ```
in the second terminal type
    ```bash
    source /opt/ros/humble/setup.bash
    ros2 run demo_nodes_py listener
    ```
it should work







1. **Stop Working and Commit**:

   - Exit the container:

     ```bash
     exit
     ```

   - Find the container ID:

     ```bash
     sudo docker ps -a
     ```

   - Commit the container:

     ```bash
     sudo docker commit <container_id> my-ros-ubuntu-22.04
     ```

2. **Start Working Again**:

   - List Docker images to verify:

     ```bash
     sudo docker images
     ```

   - Run a new container:

     ```bash
     sudo docker run -it --name my_ros_container my-ros-ubuntu-22.04 /bin/bash
     ```

3. **Open Additional Terminals**:

   - List running containers if needed:

     ```bash
     sudo docker ps
     ```

   - Open a new terminal session:

     ```bash
     sudo docker exec -it my_ros_container /bin/bash
     ```

By following these steps, you can effectively manage your Docker container workflow, ensuring your work is saved and easily resumable.