
pkgdesc="ROS - Components of MoveIt that offer simpler interfaces to planning and execution."
url='http://www.ros.org/'

pkgname='ros-hydro-moveit-ros-planning-interface'
pkgver='0.5.16'
_pkgver_patch=0
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')

ros_makedepends=(ros-hydro-moveit-ros-planning
  ros-hydro-moveit-ros-manipulation
  ros-hydro-rosconsole
  ros-hydro-eigen-conversions
  ros-hydro-rospy
  ros-hydro-moveit-ros-warehouse
  ros-hydro-moveit-ros-move-group
  ros-hydro-tf-conversions
  ros-hydro-roscpp
  ros-hydro-catkin
  ros-hydro-actionlib
  ros-hydro-tf)
makedepends=('cmake' 'git' 'ros-build-tools'
  ${ros_makedepends[@]}
  python2-catkin_pkg
  python2)

ros_depends=(ros-hydro-moveit-ros-planning
  ros-hydro-moveit-ros-manipulation
  ros-hydro-rosconsole
  ros-hydro-eigen-conversions
  ros-hydro-rospy
  ros-hydro-moveit-ros-warehouse
  ros-hydro-moveit-ros-move-group
  ros-hydro-tf-conversions
  ros-hydro-roscpp
  ros-hydro-actionlib
  ros-hydro-tf)
depends=(${ros_depends[@]}
  python2)

_tag=release/hydro/moveit_ros_planning_interface/${pkgver}-${_pkgver_patch}
_dir=moveit_ros_planning_interface
source=("${_dir}"::"git+https://github.com/ros-gbp/moveit_ros-release.git"#tag=${_tag})
md5sums=('SKIP')

build() {
  # Use ROS environment variables
  /usr/share/ros-build-tools/clear-ros-env.sh
  [ -f /opt/ros/hydro/setup.bash ] && source /opt/ros/hydro/setup.bash

  # Create build directory
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build

  # Fix Python2/Python3 conflicts
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/${_dir}

  # Build project
  cmake ${srcdir}/${_dir} \
        -DCMAKE_BUILD_TYPE=Release \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/hydro \
        -DPYTHON_EXECUTABLE=/usr/bin/python2 \
        -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 \
        -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
