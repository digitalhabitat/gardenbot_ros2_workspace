#FROM althack/ros2:foxy-dev 
FROM ros

ENV UDEV=on

# ** [Optional] Uncomment this section to install additional packages. **
#
# ENV DEBIAN_FRONTEND=noninteractive
# RUN apt-get update \
#    && apt-get -y install --no-install-recommends <your-package-list-here> \
#    #
#    # Clean up
#    && apt-get autoremove -y \
#    && apt-get clean -y \
#    && rm -rf /var/lib/apt/lists/*
# ENV DEBIAN_FRONTEND=dialog

# install ros_demo_nodes package https://hub.docker.com/r/amd64/ros/
#RUN apt-get update && \
      #apt-get install -y \
      #ros-${ROS_DISTRO}-demo-nodes-cpp \
      #ros-${ROS_DISTRO}-demo-nodes-py \
      #cargo && \
      #rm -rf /var/lib/apt/lists/*

# add alias commands
# RUN printf "\n# add alias command\nalias tldr='function _(){ curl cheat.sh/\$1; }; _'\n" >> /home/ros/.bashrc

#RUN printf "alias rospeak='ros2 topic pub /chatter std_msgs/String \"data: hello\"'\n" >> /home/ros/.bashrc
#RUN printf "alias roslisten='ros2 topic echo /chatter'\n\n" >> /home/ros/.bashrc

# Set up auto-source of workspace for ros user
#ARG WORKSPACE
#RUN echo "if [ -f ${WORKSPACE}/install/setup.bash ]; then source ${WORKSPACE}/install/setup.bash; fi" >> /home/ros/.bashrc

###########################################
# Create a non-root user
###########################################
ARG USERNAME=ros
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create a non-root user
RUN groupadd --gid $USER_GID $USERNAME \
  && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
  # [Optional] Add sudo support for the non-root user
  && apt-get update \
  && apt-get install -y sudo \
  && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME\
  && chmod 0440 /etc/sudoers.d/$USERNAME \
  # Cleanup
  && rm -rf /var/lib/apt/lists/* \
  && echo "source /usr/share/bash-completion/completions/git" >> /home/$USERNAME/.bashrc \
  && echo "if [ -f /opt/ros/${ROS_DISTRO}/setup.bash ]; then source /opt/ros/${ROS_DISTRO}/setup.bash; fi" >> /home/$USERNAME/.bashrc


###########################################
# blink1-tool build depencies
# /etc/udev/rules.d is mounted via devcontainer.json
###########################################
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update \
    && apt-get install -y \
      libudev-dev \
      udev
ENV DEBIAN_FRONTEND=

###########################################
# libcamera build dependencies
# https://forums.raspberrypi.com/viewtopic.php?t=325755
###########################################
# ENV DEBIAN_FRONTEND noninteractive
# RUN sudo apt-get update \
    #  && sudo apt-get install -y \
      #  libboost-dev \
      #  libgnutls28-dev openssl libtiff5-dev \
      #  qtbase5-dev libqt5core5a libqt5gui5 libqt5widgets5 \
      #  meson \
      #  libglib2.0-dev libgstreamer-plugins-base1.0-dev \
      #  python3-pip \
    #  && pip3 install pyyaml ply \
    #  && pip3 install --upgrade meson
# ENV DEBIAN_FRONTEND=dialog

###########################################
# libcamera-apps build dependencies
###########################################
# ENV DEBIAN_FRONTEND noninteractive
# RUN sudo apt-get update \
    #  && sudo apt-get install -y \
      #  libcamera0 \
      #  libcamera-dev \
      #  python3 \
      #  v4l-utils \
      #  cmake \
      #  libboost-program-options-dev \
      #  libdrm-dev \
      #  libexif-dev
# ENV DEBIAN_FRONTEND=dialog

###########################################
# roboclaw_python_library dependencies
###########################################
ENV DEBIAN_FRONTEND noninteractive
RUN sudo apt-get update \
      && sudo apt-get install -y \
        python3-pip \
      && pip3 install pyserial
ENV DEBIAN_FRONTEND=

###########################################
# Set up auto-source of workspace for ros user 
###########################################
ARG WORKSPACE
RUN echo "if [ -f ${WORKSPACE}/install/setup.bash ]; then source ${WORKSPACE}/install/setup.bash; fi" >> /home/ros/.bashrc