# Ubuntu 20.04 LTS (Focal Fossa) é requisito para o ROS-Foxy
FROM ubuntu:20.04

# Mantenedor
LABEL maintainer="Fábio Demo <faberdemo@gmail.com>"

# Evitar perguntas durante instalação de pacotes
ENV DEBIAN_FRONTEND=noninteractive

# Atualizar a lista de pacotes e instalar pacotes básicos
RUN apt-get update -y && apt-get install -y \
    lsb-release \
    gnupg2 \
    wget \
    && rm -rf /var/lib/apt/lists/*

RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list' \
    && apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654 \
    && apt-get update

# Configurar o repositório ROS e as chaves
RUN sh -c 'echo "deb http://packages.ros.org/ros2/ubuntu `lsb_release -cs` main" > /etc/apt/sources.list.d/ros2-latest.list'
RUN wget -qO - https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add -

# Install ROS 2 on Remote PC
RUN wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros2_foxy.sh &&\
    chmod 755 ./install_ros2_foxy.sh &&\ 
    bash ./install_ros2_foxy.sh

# Install Dependent ROS 2 Packages
RUN apt-get update && apt-get install -y \
    ros-foxy-desktop
RUN ros-foxy-cartographer 
RUN ros-foxy-cartographer-ros
RUN ros-foxy-navigation2 
RUN ros-foxy-nav2-bringup

# Building TurtleBot3 package from source
RUN mkdir -p ~/turtlebot3_ws/src && \
    cd ~/turtlebot3_ws/src/ &&\
    git clone -b foxy-devel https://github.com/ROBOTIS-GIT/DynamixelSDK.git && \
    git clone -b foxy-devel https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git && \
    git clone -b foxy-devel https://github.com/ROBOTIS-GIT/turtlebot3.git && \
    cd ~/turtlebot3_ws && \
    colcon build --symlink-install && \
    echo 'source ~/turtlebot3_ws/install/setup.bash' >> ~/.bashrc
    

# Install Simulation Package
RUN source ~/.bashrc && \
    cd ~/turtlebot3_ws/src/ && \
    git clone -b foxy-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git && \
    cd ~/turtlebot3_ws && colcon build --symlink-install

# Entrypoint
CMD ["bash"]