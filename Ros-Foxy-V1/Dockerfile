# Ubuntu 20.04 LTS (Focal Fossa) é requisito para o ROS-Foxy
FROM ubuntu:20.04

# Mantenedor
LABEL maintainer="Fábio Demo <faberdemo@gmail.com>"

# Evitar perguntas durante instalação de pacotes
ENV DEBIAN_FRONTEND=noninteractive

# Atualizar a lista de pacotes e instalar pacotes básicos
RUN apt-get update && apt-get install -y \
    lsb-release \
    sudo \
    gnupg2 \
    wget \
    && rm -rf /var/lib/apt/lists/*

# Configurar o repositório ROS e as chaves
RUN sh -c 'echo "deb http://packages.ros.org/ros2/ubuntu `lsb_release -cs` main" > /etc/apt/sources.list.d/ros2-latest.list'
RUN wget -qO - https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add -

# Instalar o ROS Foxy
RUN apt-get update && apt-get install -y \
    ros-foxy-desktop \
    ros-foxy-turtlebot3-gazebo \
    && rm -rf /var/lib/apt/lists/*

# Configurar o ambiente ROS
RUN echo "source /opt/ros/foxy/setup.bash" >> /root/.bashrc

# Instalar o Gazebo
RUN apt-get update && apt-get install -y \
    gazebo11 \
    && rm -rf /var/lib/apt/lists/*

# Configurar o ambiente Gazebo
RUN echo "source /usr/share/gazebo-11/setup.sh" >> /root/.bashrc

# Entrypoint
CMD ["bash"]