# Maintainer : jopejoe1 <johannes@joens.email>

_pkgname=srmd-ncnn-vulkan
pkgname=python-$_pkgname-git
pkgver=1.0.2.2.r0.g397b85e
pkgrel=1
pkgdesc="A Python FFI of nihui/$_pkgname achieved with SWIG "
url="https://github.com/media2x/$_pkgname-python"
arch=("any")
license=("MIT")
depends=(
	"python"
	"vulkan-headers"
	"vulkan-icd-loader"
	"swig"
	"python-pillow"
)
makedepends=(
	"cmake"
	"git"
	"python-cmake-build-extension"
)
provides=('python-srmd-ncnn-vulkan')
conflicts=('python-srmd-ncnn-vulkan')
source=(
	"git+https://github.com/media2x/$_pkgname-python.git"
	"git+https://github.com/nihui/$_pkgname.git"
	"git+https://github.com/Tencent/ncnn.git"
	"git+https://github.com/webmproject/libwebp.git"
	"git+https://github.com/pybind/pybind11.git"
	"git+https://github.com/KhronosGroup/glslang.git"
)
sha256sums=(
	'SKIP'
	'SKIP'
	'SKIP'
	'SKIP'
	'SKIP'
	'SKIP'
)

pkgver() {
	cd $_pkgname-python
	echo $(git describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g')
}

prepare() {
  cd $_pkgname-python
  git submodule init
  git config submodule.srmd_ncnn_vulkan_python/$_pkgname.url "$srcdir/$_pkgname"
  git submodule update

  cd srmd_ncnn_vulkan_python/$_pkgname
  git submodule init
  git config submodule.src/ncnn.url "$srcdir/ncnn"
  git config submodule.src/libwebp.url "$srcdir/libwebp"
  git submodule update

  cd src/ncnn
  git submodule init
  git config submodule.glslang.url "$srcdir/glslang"
  git config submodule.python/pybind11.url "$srcdir/pybind11"
  git submodule update
}

build() {
	cd $_pkgname-python
	python setup.py build
}

package() {
	cd $_pkgname-python
	python setup.py install --root="${pkgdir}" --optimize=1 --skip-build
}
