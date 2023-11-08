FROM osrf/ros:humble-desktop

# Instalar o pacote gazebo_ros
RUN apt-get update && apt-get install -y \
    ros-humble-gazebo-ros-pkgs && \
    rm -rf /var/lib/apt/lists/*