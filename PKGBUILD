pkgname=htop
pkgver=3.0.5
pkgrel=1
pkgdesc='An interactive process viewer for Unix'
arch=(x86_64)
url='http://htop.dev'
license=(BSD)
groups=()
depends=()
makedepends=(
    libncurses-dev
    libtool
)
options=()


source=(
    "htop-${pkgver}.tar.gz::https://github.com/htop-dev/htop/archive/refs/tags/${pkgver}.tar.gz"
)
sha256sums=(
    4c2629bd50895bd24082ba2f81f8c972348aa2298cc6edc6a21a7fa18b73990c
)


build() {
    cd_unpacked_src
    ./autogen.sh
    CFLAGS+=' --static' \
      ./configure \
      --prefix=/usr
    make
}

package() {
    cd_unpacked_src
    make DESTDIR="${pkgdir}" install
}
