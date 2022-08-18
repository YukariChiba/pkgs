pkgname=parted
pkgver=3.4
pkgrel=1
pkgdesc='partition table manipulator'
arch=(x86_64)
url='http://www.gnu.org/software/parted'
license=(GPL3)
groups=()
depends=()
makedepends=(
    libuuid-dev
    libncurses-dev
    readline-dev
)
options=()

source=(
    "http://ftp.gnu.org/gnu/${pkgname}/${pkgname}-${pkgver}.tar.xz"
)

sha256sums=(
    e1298022472da5589b7f2be1d5ee3c1b66ec3d96dfbad03dc642afd009da5342
)


build() {
    cd_unpacked_src
    sed -i 's@loff_t@off_t@g' libparted/fs/xfs/platform_defs.h
    CFLAGS+=' -fPIC --static' \
    ./configure \
      --prefix=/usr \
      --enable-static \
      --disable-shared \
      --disable-device-mapper
    make V=1
}

package() {
    pkgfiles=(
        usr/sbin
        usr/share
    )
    std_package
}
