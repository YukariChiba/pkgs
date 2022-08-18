pkgname=cmake
_major_minor=3.21
pkgver="${_major_minor}.1"
pkgrel=1
pkgdesc='The CMake toolsuite for building, testing and packaging software.'
arch=('x86_64')
url='https://cmake.org'
license=('GPL2')
groups=()
depends=()
makedepends=(openssl-dev)
options=()


source=(
    "${url}/files/v${_major_minor}/${pkgname}-${pkgver}.tar.gz"
)
sha256sums=(
    fac3915171d4dff25913975d712f76e69aef44bf738ba7b976793a458b4cfed4
)


build() {
    cd_unpacked_src
    ./bootstrap --prefix=/usr
    make
}

package() {
    pkgfiles=(
        usr/bin
        usr/share
    )
    depends=(
        "ld-musl-$(arch).so.1"
        libc++.so.1
        libc++abi.so.1
        libcrypto.so.1.1
        libssl.so.1.1
        libunwind.so.1
    )
    std_package
}
