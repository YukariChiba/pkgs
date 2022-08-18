pkgname=(
    acl
    libacl
    libacl-dev
)
pkgver=2.2.53
pkgrel=1
pkgdesc='A library for manipulating POSIX access control lists'
arch=(x86_64)
url='http://savannah.nongnu.org/projects/acl'
license=(GPL)
groups=()
depends=()
makedepends=(gettext libattr-dev)
options=()

source=(
    "http://download.savannah.gnu.org/releases/acl/acl-${pkgver}.tar.gz"
)
sha256sums=(
    06be9865c6f418d851ff4494e12406568353b891ffe1f596b34693c387af26c7
)

build() {
    cd_unpacked_src
    CFLAGS+=' -fPIC' ./configure \
      --prefix=/usr
    make
}

package_acl() {
    pkgfiles=(
        usr/bin
    )
    depends=(
        libacl.so.1
        libattr.so.1
        "ld-musl-$(arch).so.1"
    )
    std_package
}

package_libacl() {
    pkgfiles=(
        usr/lib/lib*.so.*
    )
    depends=(
        libattr.so.1
        "ld-musl-$(arch).so.1"
    )
    provides=(
        libacl.so.1
    )
    std_split_package
}

package_libacl-dev() {
    pkgfiles=(
        usr/include
        usr/lib/*.so
        usr/lib/*.a
    )
    depends=(
        "libacl=${pkgver}"
    )
    std_split_package
}
