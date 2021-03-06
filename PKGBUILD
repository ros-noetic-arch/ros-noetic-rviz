pkgdesc="ROS - 3D visualization tool for ROS."
url='https://wiki.ros.org/rviz'

pkgname='ros-noetic-rviz'
pkgver='1.14.8'
arch=('i686' 'x86_64' 'aarch64' 'armv7h' 'armv6h')
pkgrel=1
license=('BSD, Creative Commons')

ros_makedepends=(
    ros-noetic-catkin
    ros-noetic-cmake-modules
    ros-noetic-message-generation
)

makedepends=(
    cmake
    ros-build-tools
    ${ros_makedepends[@]}
    eigen
    qt5-base
    urdfdom
    urdfdom-headers
)

ros_depends=(
    ros-noetic-geometry-msgs
    ros-noetic-image-transport
    ros-noetic-interactive-markers
    ros-noetic-laser-geometry
    ros-noetic-map-msgs
    ros-noetic-message-filters
    ros-noetic-pluginlib
    ros-noetic-python-qt-binding
    ros-noetic-resource-retriever
    ros-noetic-rosbag
    ros-noetic-rosconsole
    ros-noetic-roscpp
    ros-noetic-roslib
    ros-noetic-rospy
    ros-noetic-sensor-msgs
    ros-noetic-std-msgs
    ros-noetic-std-srvs
    ros-noetic-tf2-ros
    ros-noetic-tf2-geometry-msgs
    ros-noetic-urdf
    ros-noetic-visualization-msgs
    ros-noetic-media-export
    ros-noetic-message-runtime
)

depends=(
    ${ros_depends[@]}
    assimp
    ogre=1.9
    tinyxml2
    yaml-cpp
    mesa
    qt5-base
    sip
    python-sip
)

_dir="rviz-${pkgver}/"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros-visualization/rviz/archive/${pkgver}.tar.gz")
sha256sums=('ef889654426936f9d67e1c15aa78a64e52a2e51044d1284c9f2c0beda9f399e9')

build() {
    # Use ROS environment variables.
    source /usr/share/ros-build-tools/clear-ros-env.sh
    [ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

    # Create the build directory.
    [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
    cd ${srcdir}/build

    # Build the project.
    cmake ${srcdir}/${_dir} \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
        -DPYTHON_EXECUTABLE=/usr/bin/python \
        -DSETUPTOOLS_DEB_LAYOUT=OFF

    make
}

package() {
    cd "${srcdir}/build"
    make DESTDIR="${pkgdir}/" install
}
