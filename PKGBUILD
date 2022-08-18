pkgname=(libaio libaio-dev)
pkgver=0.3.112
pkgrel=1
pkgdesc='Linux-native asynchronous I/O access library'
arch=(x86_64)
url=https://pagure.io/libaio
license=(GPL2)
groups=()
depends=()
makedepends=()
options=()

source=(
    "https://pagure.io/libaio/archive/libaio-${pkgver}/libaio-libaio-${pkgver}.tar.gz"
)
sha256sums=(
    b7cf93b29bbfb354213a0e8c0e82dfcf4e776157940d894750528714a0af2272
)


build() {
    cd_unpacked_src
    make prefix=/usr
}

package_libaio() {
    pkgfiles=(
        usr/lib/libaio.so.*
    )
    depends=(
        libc.so
        ld-musl-$(arch).so.1
    )
    provides=(
        libaio.so.1.0.1
    )
    cd_unpacked_src
    make prefix=/usr DESTDIR="${pkgdirbase}/dest" install
    std_split_package
}

package_libaio-dev() {
    pkgfiles=(
        usr/include
        usr/lib/libaio.so
        usr/lib/libaio.a
    )
    depends=(libaio.so.1.0.1)
    std_split_package
}
