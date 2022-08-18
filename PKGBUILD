pkgname=(zlib zlib-dev)
pkgver=1.2.11
pkgrel=1
pkgdesc='A Massively Spiffy Yet Delicately Unobtrusive Compression Library'
arch=(x86_64)
url='http://www.zlib.net'
license=(BSD)
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
    LDSHARED="cc -shared -Wl,-soname,libz.so.1,--version-script,zlib.map" \
        ./configure --prefix=/usr
    make
}

package_zlib() {
    pkgfiles=(
        usr/lib/lib*.so.*
    )
    depends=(
        "ld-musl-$(arch).so.1"
    )
    provides=(
        libz.so.1
    )
    std_package
}

package_zlib-dev() {
    pkgfiles=(
        usr/include
        usr/lib/lib*.a
        usr/lib/lib*.so
        usr/lib/pkgconfig
    )
    depends=(
        "zlib=${pkgver}"
    )
    std_split_package
}
