FROM althack/ros2:foxy-dev 

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
RUN printf "\n# add alias command\nalias tldr='function _(){ curl cheat.sh/\$1; }; _'\n" >> /home/ros/.bashrc
RUN printf "alias rospeak='ros2 topic pub /chatter std_msgs/String \"data: hello\"'\n" >> /home/ros/.bashrc
RUN printf "alias roslisten='ros2 topic echo /chatter'\n\n" >> /home/ros/.bashrc

# Set up auto-source of workspace for ros user
ARG WORKSPACE
RUN echo "if [ -f ${WORKSPACE}/install/setup.bash ]; then source ${WORKSPACE}/install/setup.bash; fi" >> /home/ros/.bashrc
