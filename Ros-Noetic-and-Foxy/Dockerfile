# Ubuntu 20.04 LTS (Focal Fossa) é requisito para o ROS-Foxy
FROM ubuntu:20.04

# Mantenedor
LABEL maintainer="Fábio Demo <faberdemo@gmail.com>"

# Evitar perguntas durante instalação de pacotes
ENV DEBIAN_FRONTEND=noninteractive

# Atualizar a lista de pacotes e instalar pacotes básicos
RUN apt-get update && apt-get install -y \
    lsb-release \
    gnupg2 \
    wget \
    && rm -rf /var/lib/apt/lists/*

# Install ROS 2 on Remote PC
RUN wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros2_foxy.sh \
    chmod 755 ./install_ros2_foxy.sh \ 
    bash ./install_ros2_foxy.sh

# Install Dependent ROS 2 Packages
RUN apt-get install ros-foxy-gazebo-* \
    ros-foxy-cartographer \
    ros-foxy-cartographer-ros \
    ros-foxy-navigation2 \
    ros-foxy-nav2-bringup

# Building TurtleBot3 package from source (Install TurtleBot3 Packages)
RUN mkdir -p ~/turtlebot3_ws/src \
    cd ~/turtlebot3_ws/src/ \
    git clone -b foxy-devel https://github.com/ROBOTIS-GIT/DynamixelSDK.git \
    git clone -b foxy-devel https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git \
    git clone -b foxy-devel https://github.com/ROBOTIS-GIT/turtlebot3.git \
    cd ~/turtlebot3_ws \
    colcon build --symlink-install \
    echo 'source ~/turtlebot3_ws/install/setup.bash' >> ~/.bashrc \
    source ~/.bashrc
    

# Install Simulation Package
RUN cd ~/turtlebot3_ws/src/ \
    git clone -b foxy-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git \
    cd ~/turtlebot3_ws && colcon build --symlink-install

# Entrypoint
CMD ["bash"]