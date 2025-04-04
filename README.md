# Desktop

This repository contains the setup for running an Ubuntu desktop environment with ROS 2 and VNC in a GitHub Codespace.

## Why Use This Docker Image?

When working with ROS 2 projects, we often need to use multiple ROS 2 distributions and different versions of Ubuntu Linux. This can make it challenging to maintain a clean and consistent codebase.

For example, if you are an educator conducting a training or workshop, participants may have diverse hardware, operating systems, and configurations. This variability can complicate the setup process.

### The Solution

What if you could have the entire graphical ROS 2 environment, including simulation, running in a web browser? No dependencies on the host system, and compatible with multiple operating systems—all with a single command.

If this sounds appealing, check out the Docker images repository: [ROS 2 Docker Images](https://lnkd.in/dJ2_4vaE).

These images allow you to:
- Run ROS 2 on any operating system.
- Maintain a clean, identical environment for all users.
- Simplify setup with just one command.

## Setup Instructions

This setup is specifically designed for GitHub Codespaces and includes installing the XFCE desktop environment within the Codespaces environment.

### 1. Install Docker in Codespaces
Before running, building, or pulling the Docker image, ensure Docker is installed in your Codespaces environment:
```bash
sudo apt-get update
sudo apt-get install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
```
*(Note: If installation fails due to dependencies, try `sudo apt-get update && sudo apt-get install -y containerd && sudo apt-get install -y docker.io`)*

### 2. Pull the Docker Image
Before starting the container, pull the Docker image:
```bash
docker pull rgruberski/ros2-ubuntu-web-vnc:humble
```

### 3. Start the Docker Container
```bash
# The --security-opt seccomp=unconfined flag may be needed in some environments (like Codespaces) 
# to allow the desktop environment within the container to start correctly.
docker run --name ros2-humble-vnc --security-opt seccomp=unconfined -p 8080:8080 -p 5900:5900 -d rgruberski/ros2-ubuntu-web-vnc:humble
```

### 4. Install XFCE Desktop Environment
XFCE is installed directly in the Codespaces environment:
```bash
sudo apt-get update
sudo apt-get install -y xfce4 xfce4-goodies
```

### 5. Restart the VNC Server
```bash
vncserver -kill :1
vncserver :1
```

### 6. Forward Ports in Codespaces
- Open the **Ports** tab in the Codespaces interface.
- Ensure port `8080` (for the web-based VNC viewer) is forwarded and set to **Public**.

### 7. Access the Web VNC Viewer
- Open your browser and navigate to:
  ```
  https://<your-codespace-id>-8080.githubpreview.dev
  ```
- You should now see the XFCE desktop environment.

### 8. Run Applications
Use the terminal in the XFCE desktop to run applications like `rviz2` or any other tools you need.

---
