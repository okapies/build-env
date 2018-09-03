FROM centos:5
MAINTAINER Yuta Okamoto <okapies@gmail.com>

RUN sed -i 's/enabled=1/enabled=0/' /etc/yum/pluginconf.d/fastestmirror.conf && \
    sed -i 's/mirrorlist/#mirrorlist/' /etc/yum.repos.d/*.repo && \
    sed -i 's|#baseurl=http://mirror.centos.org/centos/$releasever|baseurl=http://vault.centos.org/5.11|' /etc/yum.repos.d/*.repo

RUN yum -y install make gcc gcc-c++ glibc-devel perl wget bzip2 curl && \
    rm -rf /var/lib/apt/lists/*

RUN cd /usr/local/src && \
    echo 'b92b423b2f8f517c909fda2621ff2d7c  gcc-4.9.4.tar.gz' > gcc-4.9.4.tar.gz.md5 && \
    wget http://www.netgull.com/gcc/releases/gcc-4.9.4/gcc-4.9.4.tar.gz && \
    md5sum -c gcc-4.9.4.tar.gz.md5 && \
    tar xvzf gcc-4.9.4.tar.gz && \
    cd gcc-4.9.4 && \
    ./contrib/download_prerequisites && \
    mkdir -p build && \
    cd build && \
    ../configure --prefix=/usr/local/gcc-4.9.4 CXXFLAGS=-fPIC CFLAGS=-fPIC --enable-languages=c,c++ && \
    make && \
    make install && \
    cd / && \
    rm -rf /usr/local/src/gcc-4.9.4 && \
    rm /usr/local/src/gcc-4.9.4.tar.gz*

RUN cd /usr/local/src && \
    echo '10109246a51102bfda45ff3935275fbf  cmake-3.12.1.tar.gz' > cmake-3.12.1.tar.gz.md5 && \
    wget https://cmake.org/files/v3.12/cmake-3.12.1.tar.gz && \
    md5sum -c cmake-3.12.1.tar.gz.md5 && \
    tar xvzf cmake-3.12.1.tar.gz && \
    cd cmake-3.12.1 && \
    CC=/usr/local/gcc-4.9.4/bin/gcc CXX=/usr/local/gcc-4.9.4/bin/g++ ./bootstrap && \
    make && \
    make install && \
    rm -rf /usr/local/src/cmake-3.12.1 && \
    rm cmake-3.12.1.tar.gz*

ENV PATH /usr/local/gcc-4.9.4/bin:$PATH
ENV LD_LIBRARY_PATH /usr/local/gcc-4.9.4/lib64/:$LD_LIBRARY_PATH
