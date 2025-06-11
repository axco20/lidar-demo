# Use Ubuntu 22.04 as a base
FROM ubuntu:22.04

# avoid interactive prompts
ENV DEBIAN_FRONTEND=noninteractive

# install basics + ROS2 Humble + Gazebo
RUN apt-get update && apt-get install -y \
    locales \
    curl \
    gnupg2 \
    lsb-release \
    build-essential \
    python3-pip \
    # ROS2 Humble keys/repos
    && curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key | apt-key add - \
    && echo "deb http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros2.list \
    && apt-get update && apt-get install -y \
    ros-humble-desktop \
    ros-humble-turtlebot3-gazebo \
    && rm -rf /var/lib/apt/lists/*

# set up locale & ROS environment
RUN locale-gen en_US en_US.UTF-8 && update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
ENV LANG=en_US.UTF-8  
ENV ROS_DISTRO=humble
ENV TURTLEBOT3_MODEL=burger

# ROS entrypoint
COPY .bashrc /root/.bashrc
RUN echo "source /opt/ros/humble/setup.bash" >> /root/.bashrc

# workspace folder
WORKDIR /workspace
