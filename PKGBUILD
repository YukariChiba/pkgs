pkgname=(blkid libblkid-dev libuuid-dev)
pkgver=2.37.2
pkgrel=1
pkgdesc='A command-line utility to locate/print block device attributes'
arch=(x86_64)
url=https://github.com/karelzak/util-linux
license=(GPL)
groups=()
depends=()
makedepends=(
    bison
    gettext
    libtool
)
options=()

source=(
    "util-linux-${pkgver}.tar.gz::https://github.com/karelzak/util-linux/archive/refs/tags/v${pkgver}.tar.gz"
)

sha256sums=(
    74e725802a6355bba7288caeca171e0e25d9da2aa570162efbc1397ed924dfa2
)

build() {
    cd_unpacked_src
    ./autogen.sh
    CFLAGS+=' --static' \
    ./configure --prefix=/usr \
        --enable-static \
        --disable-shared
    make
}

package_blkid() {
    pkgfiles=(
        sbin/blkid
    )
    std_package
}

package_libblkid-dev() {
    pkgfiles=(
        usr/include/blkid
        usr/lib/pkgconfig/blkid.pc
        usr/lib/libblkid.a
    )
    std_split_package
}

package_libuuid-dev() {
    pkgfiles=(
        usr/include/uuid
        usr/lib/pkgconfig/uuid.pc
        usr/lib/libuuid.a
    )
    std_split_package
}
