pkgname=kpartx
pkgver=0.8.6
pkgrel=1
pkgdesc='Tools for the Device Mapper multipathing driver'
arch=(x86_64)
url='http://christophe.varoqui.free.fr/'
license=(GPL2)
groups=()
depends=()
makedepends=(
    libdevmapper-dev
)
options=()

source=(
    "kpartx-${pkgver}.tar.gz::https://github.com/opensvc/multipath-tools/archive/refs/tags/${pkgver}.tar.gz"
)
sha256sums=(
    ba781d981bd6e8efa5f9f3af6727f85520af6395958e852c1907f59f6124f08e
)


build() {
    cd_unpacked_src
    make -C kpartx VERSION=$pkgver LDFLAGS='-static -Wl,-static -ldevmapper'
}

package() {
    cd_unpacked_src
    install -d "${pkgdir}/usr/sbin" "${pkgdir}/usr/share/man/man8"
    install -m 0755 kpartx/kpartx "${pkgdir}/usr/sbin/kpartx"
    install -m 0644 kpartx/kpartx.8 "${pkgdir}/usr/share/man/man8/"
}
