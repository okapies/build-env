FROM centos:centos6
MAINTAINER Yuta Okamoto <okapies@gmail.com>

RUN yum -y install make gcc gcc-c++ texinfo-tex flex zip libgcc.x86_64 glibc-devel.x86_64 \
        autoconf automake libtool unzip perl wget bzip2 curl git && \
    yum -y install epel-release && \
    rm -rf /var/lib/apt/lists/*

RUN cd /usr/local/src && \
    wget http://www.netgull.com/gcc/releases/gcc-8.2.0/gcc-8.2.0.tar.gz && \
    echo '1b0f36be1045ff58cbb9c83743835367b860810f17f0195a4e093458b372020f  gcc-8.2.0.tar.gz' > gcc-8.2.0.tar.gz.sha256 && \
    sha256sum -c gcc-8.2.0.tar.gz.sha256 && \
    tar -zxf gcc-8.2.0.tar.gz && \
    cd gcc-8.2.0 && \
    ./contrib/download_prerequisites && \
    mkdir -p build && \
    cd build && \
    ../configure --prefix=/usr/local/gcc-8.2.0 CFLAGS=-fPIC CXXFLAGS=-fPIC --enable-languages=c,c++ --disable-bootstrap --disable-multilib && \
    make -j$(nproc) && \
    make install && \
    cd / && \
    rm -rf /usr/local/src/gcc-8.2.0 && \
    rm /usr/local/src/gcc-8.2.0.tar.gz*

ENV PATH /usr/local/gcc-8.2.0/bin:$PATH
ENV LD_LIBRARY_PATH /usr/local/gcc-8.2.0/lib64:/usr/local/gcc-8.2.0/lib:/usr/local/lib64:/usr/local/lib:$LD_LIBRARY_PATH

RUN yum -y install cmake && \
    cd /usr/local/src && \
    wget https://cmake.org/files/v3.12/cmake-3.12.1.tar.gz && \
    echo 'c53d5c2ce81d7a957ee83e3e635c8cda5dfe20c9d501a4828ee28e1615e57ab2  cmake-3.12.1.tar.gz' > cmake-3.12.1.tar.gz.sha256 && \
    sha256sum -c cmake-3.12.1.tar.gz.sha256 && \
    tar -zxf cmake-3.12.1.tar.gz && \
    cd cmake-3.12.1 && \
    cmake -DCMAKE_BUILD_TYPE=Release . && \
    make -j$(nproc) && \
    make install && \
    cd / && \
    yum -y erase cmake && \
    rm -rf /usr/local/src/cmake-3.12.1 && \
    rm /usr/local/src/cmake-3.12.1.tar.gz*
