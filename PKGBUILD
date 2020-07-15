pkgdesc="ROS - Low-level build system macros and infrastructure for ROS."
url='https://wiki.ros.org/catkin'

pkgname='ros-noetic-catkin'
pkgver='0.8.7'
arch=('any')
pkgrel=1
license=('BSD')

ros_makedepends=(
)

makedepends=(
	cmake
	${ros_makedepends[@]}
	python-catkin-pkg
	python-empy
	python
)

ros_depends=(
)

depends=(
	${ros_depends[@]}
	python-nose
	gtest
	python-catkin-pkg
	python-empy
	gmock
	python
	ros-build-tools
)

_dir="catkin-${pkgver}"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros/catkin/archive/${pkgver}.tar.gz")
sha256sums=('cffc3d336d9478cb172ec05afee3f003c6e8407076e06eb703ec39e778b2f81c')

build() {
	# Use ROS environment variables.
	source /usr/share/ros-build-tools/clear-ros-env.sh
	[ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

	# Create the build directory.
	[ -d ${srcdir}/build ] || mkdir ${srcdir}/build
	cd ${srcdir}/build

	# Build the project.
	cmake ${srcdir}/${_dir} \
		-DCATKIN_BUILD_BINARY_PACKAGE=OFF \
		-DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
		-DPYTHON_EXECUTABLE=/usr/bin/python \
		-DSETUPTOOLS_DEB_LAYOUT=OFF
	make
}

package() {
	cd "${srcdir}/build"
	make DESTDIR="${pkgdir}/" install
}
