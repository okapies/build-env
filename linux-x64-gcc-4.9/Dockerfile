FROM okapies/buildenv:linux-x64-gcc-4.9-base
MAINTAINER Yuta Okamoto <okapies@gmail.com>

# Install additional toolchains to the base image

## CMake
RUN yum install -y zlib-devel curl-devel && \
    yum clean -y all

RUN cd /usr/local/src && \
    wget https://cmake.org/files/v3.12/cmake-3.12.2.tar.gz && \
    echo '0f97485799e51a7070cc11494f3e02349b0fc3a24cc12b082e737bf67a0581a4  cmake-3.12.2.tar.gz' > cmake-3.12.2.tar.gz.sha256 && \
    sha256sum -c cmake-3.12.2.tar.gz.sha256 && \
    tar -zxf cmake-3.12.2.tar.gz && \
    cd cmake-3.12.2 && \
    ./bootstrap --parallel=$(nproc) --system-curl && \
    make -j$(nproc) && \
    make install && \
    cd / && \
    rm -rf /usr/local/src/cmake-3.12.2 && \
    rm /usr/local/src/cmake-3.12.2.tar.gz*

## Python
RUN yum install -y https://centos6.iuscommunity.org/ius-release.rpm && \
    yum install -y python36u python36u-libs python36u-devel python36u-pip && \
    ln -s /usr/bin/python3.6 /usr/bin/python3 && \
    ln -s /usr/bin/python3.6m /usr/bin/python3m && \
    ln -s /usr/bin/pydoc3.6 /usr/bin/pydoc3 && \
    ln -s /usr/bin/pip3.6 /usr/bin/pip3 && \
    yum clean -y all

## OpenCV
RUN yum install -y gtk2-devel pkconfig ffmpeg && \
    pip3 install numpy && \
    yum clean -y all

RUN cd /usr/local/src && \
    wget -O opencv-3.4.3.zip https://github.com/opencv/opencv/archive/3.4.3.zip && \
    echo '37c7d8c3b9807902ad11b9181bbde61dcb3898a78a563130494752f46fe8cc5f  opencv-3.4.3.zip' > opencv-3.4.3.zip.sha256 && \
    sha256sum -c opencv-3.4.3.zip.sha256 && \
    unzip opencv-3.4.3.zip && \
    cd opencv-3.4.3 && \
    mkdir -p build && \
    cd build && \
    cmake \
        -DCMAKE_BUILD_TYPE=Release \
        -DCMAKE_INSTALL_PREFIX=/usr/local \
        -DPYTHON_DEFAULT_EXECUTABLE=/usr/bin/python3 \
        -DBUILD_opencv_python2=OFF \
        -DBUILD_opencv_python3=ON \
        -DPYTHON3_LIBRARY=/usr/lib64/libpython3.6m.so \
        -DPYTHON3_INCLUDE_DIR=/usr/include/python3.6m \ 
        -DPYTHON3_PACKAGES_PATH=/usr/lib/python3.6/site-packages \
        -DPYTHON3_EXECUTABLE=/usr/bin/python3 \
        -DCPU_BASELINE=SSE4_2 \
        -DCPU_DISPATCH= \
        -DBUILD_EXAMPLES=OFF \
        -DBUILD_TESTS=OFF \
        -DBUILD_PERF_TESTS=OFF \
        .. && \
    make -j$(nproc) && \
    make install && \
    cd / && \
    rm -rf /usr/local/src/opencv-3.4.3 && \
    rm /usr/local/src/opencv-3.4.3.zip*
