# Desktop

This repository contains the setup for running an Ubuntu desktop environment with ROS 2 and VNC in a GitHub Codespace.

## Setup Instructions

Follow these steps to set up the Codespace with an Ubuntu desktop environment accessible via VNC:

### 1. Start the Docker Container
```bash
docker run --name ros2-humble-vnc -p 8080:8080 -p 5900:5900 -d rgruberski/ros2-ubuntu-web-vnc:humble
```

### 2. Install XFCE Desktop Environment
```bash
sudo apt-get update
sudo apt-get install -y xfce4 xfce4-goodies
```

### 3. Restart the VNC Server
```bash
vncserver -kill :1
vncserver :1
```

### 4. Forward Ports in Codespaces
- Open the **Ports** tab in the Codespaces interface.
- Ensure port `8080` (for the web-based VNC viewer) is forwarded and set to **Public**.

### 5. Access the Web VNC Viewer
- Open your browser and navigate to:
  ```
  https://<your-codespace-id>-8080.githubpreview.dev
  ```
- You should now see the XFCE desktop environment.

### 6. Run Applications
Use the terminal in the XFCE desktop to run applications like `rviz2` or any other tools you need.

---