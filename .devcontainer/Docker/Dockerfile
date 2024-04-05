FROM ros:noetic-robot

RUN apt-get update

# Install packages
RUN apt-get install -y \
    sudo \
    build-essential \
    cmake \
    git \
    net-tools \
    iputils-ping \
    cmake-curses-gui \
    subversion \
    wget \
    # Recommended ViSP 3rd parties
    libopencv-dev \
    libx11-dev \
    liblapack-dev \
    libeigen3-dev \
    libv4l-dev \
    libzbar-dev \
    libpthread-stubs0-dev \
    libdc1394-22-dev \
    nlohmann-json3-dev 
    # Other optional 3rd parties



# Installing visp 

# Install visp-images
RUN mkdir -p ${HOME}/visp-ws \
    && cd ${HOME}/visp-ws \
    && git clone https://github.com/lagadic/visp-images.git \
    && echo "export VISP_WS=${HOME}/visp-ws" >> ${HOME}/.bashrc \
    && echo "export VISP_INPUT_IMAGE_PATH=${HOME}/visp-ws/visp-images" >> ${HOME}/.bashrc

# Get visp
RUN cd ${HOME}/visp-ws \
    && git clone https://github.com/lagadic/visp

# Build visp
RUN cd ${HOME}/visp-ws \
    && mkdir visp-build \
    && cd visp-build \
    && cmake ../visp \
    && make -j4


# Build libealsense

RUN apt-get install -y \
    udev \
    libssl-dev \
    libusb-1.0-0-dev \
    pkg-config \
    libgtk-3-dev \
    libglfw3-dev \
    libgl1-mesa-dev \
    libglu1-mesa-dev \
    at \
    libudev-dev \
    libgtk-3-dev 
    

RUN mkdir -p ${HOME}/visp-ws/3rdparty \
    && cd ${HOME}/visp-ws/3rdparty \
    && git clone https://github.com/IntelRealSense/librealsense.git \
    && cd librealsense \
    && sudo ./scripts/setup_udev_rules.sh

RUN cd ${HOME}/visp-ws/3rdparty/librealsense \
    && mkdir build \
    && cd build \
    && cmake .. -DBUILD_EXAMPLES=TRUE -DCMAKE_BUILD_TYPE=Release \
    && make -j4 \
    && sudo make install

RUN apt-get install -y \
    ros-noetic-libfranka \
    ros-noetic-franka-ros
