FROM centos:centos6
MAINTAINER Yuta Okamoto <okapies@gmail.com>

RUN yum -y install make gcc gcc-c++ texinfo-tex flex zlib-devel zip libgcc.x86_64 glibc-devel.x86_64 \
        autoconf automake libtool unzip patch perl wget bzip2 curl git && \
    yum -y install epel-release && \
    rm -rf /var/lib/apt/lists/*

RUN cd /usr/local/src && \
    wget http://www.netgull.com/gcc/releases/gcc-6.4.0/gcc-6.4.0.tar.gz && \
    echo '4715f02413f8a91d02d967521c084990c99ce1a671b8a450a80fbd4245f4b728  gcc-6.4.0.tar.gz' > gcc-6.4.0.tar.gz.sha256 && \
    sha256sum -c gcc-6.4.0.tar.gz.sha256 && \
    tar -zxf gcc-6.4.0.tar.gz && \
    cd gcc-6.4.0 && \
    ./contrib/download_prerequisites && \
    mkdir -p build && \
    cd build && \
    ../configure --prefix=/usr/local/gcc-6.4.0 \
        --disable-bootstrap \
        --enable-shared \
        --enable-threads=posix \
        --enable-checking=release \
        --with-system-zlib \
        --enable-__cxa_atexit \
        --disable-libunwind-exceptions \
        --enable-gnu-unique-object \
        --enable-linker-build-id \
        --with-linker-hash-style=gnu \
        --enable-languages=c,c++ \
        --enable-plugin \
        --enable-initfini-array \
        --disable-libgcj \
        --with-tune=generic \
        --build=x86_64-linux-gnu \
        --host=x86_64-linux-gnu \
        --target=x86_64-linux-gnu \
        --disable-multilib && \
    make BOOT_CFLAGS='-O2' -j$(nproc) && \
    make install && \
    cd / && \
    rm -rf /usr/local/src/gcc-6.4.0 && \
    rm /usr/local/src/gcc-6.4.0.tar.gz*

ENV PATH /usr/local/gcc-6.4.0/bin:$PATH
ENV LD_LIBRARY_PATH /usr/local/gcc-6.4.0/lib64:/usr/local/gcc-6.4.0/lib:/usr/local/lib64:/usr/local/lib:$LD_LIBRARY_PATH
