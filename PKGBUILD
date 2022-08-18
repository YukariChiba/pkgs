pkgname=(pciutils)
pkgver=3.7.0
pkgrel=1
pkgdesc='A tool for working with PCI devices'
arch=(x86_64)
url=''
license=(GPL)
groups=()
depends=()
makedepends=(zlib-dev)
options=()

source=(
    "https://www.kernel.org/pub/software/utils/pciutils/pciutils-${pkgver}.tar.xz"
)

sha256sums=(
    9d40b97be8b6a2cdf96aead5a61881d1f7e4e0da9544a9bac4fba1ae9dcd40eb
)


build() {
    cd_unpacked_src
    LDFLAGS='-Wl,-static' make PREFIX=/usr CC=cc SHAREDIR=/usr/share/pciutils/hwdata
}

package() {
    cd_unpacked_src
    make DESTDIR="${pkgdir}" PREFIX=/usr SHAREDIR=/usr/share/pciutils/hwdata install
    sed -i '/PCI_COMPRESSED_IDS=/s@=.*@=0@' "${pkgdir}/usr/sbin/update-pciids"
}
