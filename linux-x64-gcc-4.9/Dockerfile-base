FROM centos:centos6
MAINTAINER Yuta Okamoto <okapies@gmail.com>

RUN yum -y install make gcc gcc-c++ texinfo-tex flex zlib-devel zip libgcc.x86_64 glibc-devel.x86_64 \
        autoconf automake libtool unzip patch perl wget bzip2 curl git && \
    yum -y install epel-release && \
    rm -rf /var/lib/apt/lists/*

RUN cd /usr/local/src && \
    wget http://www.netgull.com/gcc/releases/gcc-4.9.4/gcc-4.9.4.tar.gz && \
    echo '1680f92781b92cbdb57d7e4f647c650678c594154cb0d707fd9a994424a9860d  gcc-4.9.4.tar.gz' > gcc-4.9.4.tar.gz.sha256 && \
    sha256sum -c gcc-4.9.4.tar.gz.sha256 && \
    tar -zxf gcc-4.9.4.tar.gz && \
    cd gcc-4.9.4 && \
    ./contrib/download_prerequisites && \
    mkdir -p build && \
    cd build && \
    ../configure --prefix=/usr/local/gcc-4.9.4 \
        --disable-bootstrap \
        --enable-shared \
        --enable-threads=posix \
        --enable-checking=release \
        --with-system-zlib \
        --enable-__cxa_atexit \
        --disable-libunwind-exceptions \
        --disable-gnu-unique-object \
        --enable-linker-build-id \
        --with-linker-hash-style=gnu \
        --enable-languages=c,c++ \
        --enable-plugin \
        --enable-initfini-array \
        --disable-libgcj \
        --with-tune=generic \
        --build=x86_64-CentOS-linux \
        --host=x86_64-CentOS-linux \
        --target=x86_64-CentOS-linux \
        --disable-multilib && \
    make BOOT_CFLAGS='-O2' -j$(nproc) && \
    make install && \
    cd / && \
    rm -rf /usr/local/src/gcc-4.9.4 && \
    rm /usr/local/src/gcc-4.9.4.tar.gz*

ENV PATH /usr/local/gcc-4.9.4/bin:$PATH
ENV LD_LIBRARY_PATH /usr/local/gcc-4.9.4/lib64:/usr/local/gcc-4.9.4/lib:/usr/local/lib64:/usr/local/lib:$LD_LIBRARY_PATH
