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

    apt upgrade

   apt install -y ros-humble-desktop

   apt install ros-humble-joint-state-publisher-gui

   apt install ros-humble-gazebo-ros-pkgs
   apt install ros-humble-slam-toolbox
   ```
4. **Sourcing the setup script**:
Replace ".bash" with your shell if you're not using bash
Possible values are: setup.bash, setup.sh, setup.zsh
    ```bash
    source /opt/ros/humble/setup.bash
    source ~/dev_ws/install/setup.bash
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


**ACTUALLY WORKING ON THE THING**
to run the program
don't forget to source before
   ```bash
      ros2 launch my_bot rsp.launch.py use_sim_time:=true
   ```

other terminal
   ```bash
   ros2 run joint_state_publisher_gui joint_state_publisher_gui
   ```
      avec gazebo
   ```bash
      ros2 launch my_bot launch_sim.launch.py
      ##alternante
      ros2 launch my_bot launch_sim.launch.py world:=src/my_bot/worlds/<CHANGE ME>

   ```
   keyboard control
   ```bash
      ros2 run teleop_twist_keyboard teleop_twist_keyboard
   ```
other terminal
   ```bash
   rviz2 
   ```




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

**GIT**
### How to Push Changes to a Remote Git Repository

1. **Open Terminal**: Open your terminal.

2. **Navigate to Your Project Directory**:
   ```bash
   cd /path/to/your/project
   ```

3. **Initialize Git (if not already initialized)**:
   ```bash
   git init
   ```

4. **Add Changes**:
   ```bash
   git add .
   ```

5. **Commit Changes**:
   ```bash
   git commit -m "Your commit message"
   ```

6. **Add Remote Repository (if not already added)**:
   ```bash
   git remote add origin https://github.com/yourusername/yourrepository.git
   ```

7. **Push Changes**:
   ```bash
   git push origin branch_name
   ```

### How to Pull Changes from a Remote Git Repository

1. **Open Terminal**: Open your terminal.

2. **Navigate to Your Project Directory**:
   ```bash
   cd /path/to/your/project
   ```

3. **Fetch All Branches**:
   ```bash
   git fetch origin
   ```

4. **Switch to the Desired Branch**:
   - If the branch exists locally:
     ```bash
     git checkout branch_name
     ```
   - If the branch does not exist locally:
     ```bash
     git checkout -b branch_name origin/branch_name
     ```

5. **Pull the Branch**:
   ```bash
   git pull origin branch_name
   ```

### Summary:

#### Push Changes:
1. Navigate to your project directory: `cd /path/to/your/project`
2. Initialize Git (if needed): `git init`
3. Add changes: `git add .`
4. Commit changes: `git commit -m "Your commit message"`
5. Add remote repository (if needed): `git remote add origin https://github.com/yourusername/yourrepository.git`
6. Push changes: `git push origin branch_name`

#### Pull Changes:
1. Navigate to your project directory: `cd /path/to/your/project`
2. Fetch all branches: `git fetch origin`
3. Switch to the desired branch:
   - If exists locally: `git checkout branch_name`
   - If not: `git checkout -b branch_name origin/branch_name`
4. Pull the branch: `git pull origin branch_name`

By following these steps, you can successfully push and pull changes to and from your remote Git repository.