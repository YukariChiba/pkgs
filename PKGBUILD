rationale='Many packages may use zlib, but libarchive in particular depends on its functionality'
pkgname=zlib-dev
pkgver=1.2.11
pkgrel=1
pkgdesc='A Massively Spiffy Yet Delicately Unobtrusive Compression Library'
arch=('x86_64')
url='http://www.zlib.net'
license=('BSD')
groups=()
depends=()
makedepends=()
options=()

source=(
    "http://zlib.net/zlib-${pkgver}.tar.xz"
)
sha256sums=(
    4ff941449631ace0d4d203e3483be9dbc9da454084111f97ea0a2114e19bf066
)


build() {
    cd_unpacked_src
    CFLAGS+=' -fPIC' ./configure --prefix=/usr
    make
}

package() {
    pkgfiles=(
        usr/include
        usr/lib/lib*.a
        usr/lib/pkgconfig
    )
    std_package
}
