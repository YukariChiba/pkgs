pkgname=strace
pkgver=5.13
pkgrel=1
pkgdesc='A diagnostic, debugging and instructional userspace tracer for Linux'
arch=(x86_64)
url='https://strace.io'
license=(BSD)
groups=()
depends=()
makedepends=()
options=()


source=(
    "https://strace.io/files/${pkgver}/strace-${pkgver}.tar.xz"
)
sha256sums=(
    5acc34888b9d510ad6ac915d4a8df08f51cf1ae920ea24649f6a4bb984d0b656
)


build() {
    cd_unpacked_src
    CFLAGS+=' -static' \
      ./configure \
      --prefix=/usr \
      --enable-mpers=no
    make
}

package() {
    cd_unpacked_src
    make DESTDIR="${pkgdir}" install
}
