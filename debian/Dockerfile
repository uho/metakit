# Build metakit Debian package

ARG baseimage
FROM $baseimage

ARG mk4dir
ARG arch

# Allow to execute also ARM binaries
COPY debian/qemu-arm-static /usr/bin

# Upgrade base system
RUN apt-get update && apt-get -y upgrade
RUN apt-get install -y tcl-dev git

# Build metakit
RUN git clone https://github.com/uho/metakit.git
RUN mkdir -p metakit/tbuild
WORKDIR metakit/tbuild
RUN GCC=g++ sh ../tcl/configure
RUN make
RUN make test

# Create Debian package
WORKDIR /
RUN mkdir -p tcl-metakit/DEBIAN
COPY debian/control-$arch tcl-metakit/DEBIAN/control
RUN mkdir -p tcl-metakit/usr/local/lib/tcltk/$mk4dir
RUN cp metakit/tbuild/pkgIndex.tcl tcl-metakit/usr/local/lib/tcltk/$mk4dir/pkgIndex.tcl
RUN cp metakit/tbuild/*.so tcl-metakit/usr/local/lib/tcltk/$mk4dir/
RUN dpkg-deb --build tcl-metakit /tmp
