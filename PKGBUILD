rationale='LXC and libarchive require libattr'
pkgname=(
    attr
    libattr
    libattr-dev
)
pkgver=2.4.48
pkgrel=1
pkgdesc='A library for manipulating filesystem extended attributes'
arch=(x86_64)
url='http://savannah.nongnu.org/projects/attr'
license=(GPL)
groups=()
depends=()
makedepends=(gettext)
options=()

source=(
    "http://download.savannah.gnu.org/releases/attr/attr-${pkgver}.tar.gz"
)
sha256sums=(
    5ead72b358ec709ed00bbf7a9eaef1654baad937c001c044fe8b74c57f5324e7
)


build() {
    std_build
}

package_attr() {
    pkgfiles=(
        bin
    )
    depends=(
        libattr.so.1
        "ld-musl-$(arch).so.1"
    )
    std_package
}

package_libattr() {
    pkgfiles=(
        lib/*.so.*
    )
    depends=(
        "ld-musl-$(arch).so.1"
    )
    provides=(
        libattr.so.1
    )
    std_split_package
}

package_libattr-dev() {
    pkgfiles=(
        include
        lib/*.a
        lib/*.so
    )
    depends=(
        "libattr=${pkgver}"
    )
    std_split_package
}
