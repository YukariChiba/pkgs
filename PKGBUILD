pkgname=(libtool libltdl libltdl-dev)
pkgver=2.4.6
pkgrel=1
pkgdesc='A generic library support script.'
arch=(x86_64)
url='http://www.gnu.org/software/libtool'
license=(GPL3)
groups=()
depends=()
makedepends=()
options=()

source=(
    "http://ftp.gnu.org/gnu/libtool/libtool-${pkgver}.tar.xz"
)

sha256sums=(
    7c87a8c2c8c0fc9cd5019e402bed4292462d00a718a7cd5f11218153bf28b26f
)


build() {
    cd_unpacked_src
    ./configure --prefix=/usr \
        --enable-static
    make
}

package_libtool() {
    pkgfiles=(
        usr/bin
        usr/share/aclocal
        usr/share/libtool
        usr/share/man/man1
    )
    depends=(
        autoconf
        automake
        bash
    )
    std_package
}

package_libltdl() {
    pkgfiles=(
        usr/lib/lib*.so.*
    )
    depends=(
        libc.so
    )
    provides=(
        libltdl.so.7.3.1
    )
    std_split_package
}

package_libltdl-dev() {
    pkgfiles=(
        usr/include
        usr/lib/lib*.a
        usr/lib/lib*.so
    )
    depends=(
        libltdl.so.7.3.1
    )
    std_split_package
}
