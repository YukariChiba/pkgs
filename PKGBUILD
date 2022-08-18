pkgname=pkgconf
pkgver=1.8.0
pkgrel=1
pkgdesc='An API-driven pkg-config replacement'
arch=(x86_64)
url='https://github.com/pkgconf/pkgconf'
license=(BSD)
groups=(build-base)
depends=()
makedepends=()
options=()

source=(
    "https://distfiles.dereferenced.org/pkgconf/pkgconf-${pkgver}.tar.xz"
)

sha256sums=(
    ef9c7e61822b7cb8356e6e9e1dca58d9556f3200d78acab35e4347e9d4c2bbaf
)


build() {
    cd_unpacked_src
    LDFLAGS='-static -Wl,-static' \
      ./configure \
      --prefix=/usr \
      --disable-shared \
      --with-system-libdir=/usr/lib \
      --with-system-includedir=/usr/include
    make
}

package() {
    cd_unpacked_src
    make DESTDIR="$pkgdir" install
    ln -s pkgconf "${pkgdir}/usr/bin/pkg-config"
}
