## Robot Package Template

This is a GitHub template. You can make your own copy by clicking the green "Use this template" button.

It is recommended that you keep the repo/package name the same, but if you do change it, ensure you do a "Find all" using your IDE (or the built-in GitHub IDE by hitting the `.` key) and rename all instances of `my_bot` to whatever your project's name is.

Note that each directory currently has at least one file in it to ensure that git tracks the files (and, consequently, that a fresh clone has direcctories present for CMake to find). These example files can be removed if required (and the directories can be removed if `CMakeLists.txt` is adjusted accordingly).
---

## MY CHANGES

Hello, welcome to my little project! Yes, I'm using a template from a content creator who really helped me get started with ROS.

This project is meant to run on Ubuntu 23.04 (Lunar Lobster).

### Step-by-Step Setup Instructions

### STEP 1: Install Docker and Set Up a Container

1. **Install Docker**:
   - Follow the instructions on this https://docs.docker.com/engine/install/ubuntu/
to install Docker on your system.
   
2. **Create a Docker Container**:
   ```bash
   sudo docker run -it \
     --name my_ros2_container \
     --env="DISPLAY" \
     --env="QT_X11_NO_MITSHM=1" \
     --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
     ubuntu:23.04
   ```

### STEP 2: Install ROS 2 Humble

- Follow the instructions on this https://lkseng.github.io/posts/2024/01/07/ros-2-humble-on-raspberrypi-5.html 
to install ROS 2 Humble.

### STEP 3: Set Up Workspace

1. **Create and Set Up Your ROS 2 Workspace**:
   ```bash
   # Inside the Docker container
   mkdir -p ~/ros2_ws/src
   cd ~/ros2_ws
   source /opt/ros/humble/setup.bash
   ```

### STEP 4: Clone My Branch from GitHub

1. **Clone the Project Repository**:
   ```bash
   # Inside the Docker container
   cd ~/ros2_ws/src
   git clone <your_project_repository_url>
   cd ~/ros2_ws
   colcon build
   ```

### Running the Project

1. **Source Your Workspace and Run RViz**:
   ```bash
   # Inside the Docker container
   source ~/ros2_ws/install/local_setup.bash
   rviz2
   ```

### Closing and Resuming Work

#### To Stop Working and Save Your Docker Container:

1. **Exit the Shell Session**:
   ```bash
   exit
   ```

2. **Stop the Docker Container**:
   ```bash
   sudo docker stop my_ros2_container
   ```

#### To Resume Working on Your Project:

1. **Start the Docker Container**:
   ```bash
   sudo docker start my_ros2_container
   ```

2. **Open a New Shell Session Inside the Running Container**:
   ```bash
   sudo docker exec -it my_ros2_container /bin/bash
   ```

3. **Navigate to Your Workspace and Source ROS 2 Setup**:
   ```bash
   cd ~/ros2_ws
   source /opt/ros/humble/setup.bash
   source ~/ros2_ws/install/local_setup.bash
   ```

4. **Continue Your Work**:
   ```bash
   ros2 launch my_bot rsp.launch.py
   ```

### Additional Notes

- Ensure that you have allowed Docker to use the host's X server with the following command on the host machine:
  ```bash
  xhost +local:root
  ```
- The provided link for installing ROS 2 Humble is very detailed and should be followed carefully to ensure all dependencies and configurations are correctly set up.

By following these steps, you and anyone else joining your project should have a smooth start. If you encounter any issues, feel free to reach out for help!

---