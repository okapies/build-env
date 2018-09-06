FROM centos:centos6
MAINTAINER Yuta Okamoto <okapies@gmail.com>

RUN yum -y install make gcc gcc-c++ texinfo-tex flex zip libgcc.x86_64 glibc-devel.x86_64 \
        autoconf automake libtool unzip perl wget bzip2 curl git && \
    yum -y install epel-release && \
    rm -rf /var/lib/apt/lists/*

RUN cd /usr/local/src && \
    wget http://www.netgull.com/gcc/releases/gcc-5.2.0/gcc-5.2.0.tar.gz && \
    echo '87f3f1b3deebee26b6b71068c37201541586647c1ee64a505b06fc4129d6376a  gcc-5.2.0.tar.gz' > gcc-5.2.0.tar.gz.sha256 && \
    sha256sum -c gcc-5.2.0.tar.gz.sha256 && \
    tar -zxf gcc-5.2.0.tar.gz && \
    cd gcc-5.2.0 && \
    ./contrib/download_prerequisites && \
    mkdir -p build && \
    cd build && \
    ../configure --prefix=/usr/local/gcc-5.2.0 CFLAGS=-fPIC CXXFLAGS=-fPIC --enable-languages=c,c++ --disable-bootstrap --disable-multilib && \
    make -j$(grep -c processor /proc/cpuinfo) && \
    make install && \
    cd / && \
    rm -rf /usr/local/src/gcc-5.2.0 && \
    rm /usr/local/src/gcc-5.2.0.tar.gz*

ENV PATH /usr/local/gcc-5.2.0/bin:$PATH
ENV LD_LIBRARY_PATH /usr/local/gcc-5.2.0/lib64:/usr/local/gcc-5.2.0/lib:/usr/local/lib64:/usr/local/lib:$LD_LIBRARY_PATH

RUN cd /usr/local/src && \
    wget https://cmake.org/files/v3.12/cmake-3.12.1.tar.gz && \
    echo 'c53d5c2ce81d7a957ee83e3e635c8cda5dfe20c9d501a4828ee28e1615e57ab2  cmake-3.12.1.tar.gz' > cmake-3.12.1.tar.gz.sha256 && \
    sha256sum -c cmake-3.12.1.tar.gz.sha256 && \
    tar -zxf cmake-3.12.1.tar.gz && \
    cd cmake-3.12.1 && \
    ./bootstrap --parallel=$(grep -c processor /proc/cpuinfo) && \
    make -j$(grep -c processor /proc/cpuinfo) && \
    make install && \
    cd / && \
    rm -rf /usr/local/src/cmake-3.12.1 && \
    rm /usr/local/src/cmake-3.12.1.tar.gz*
