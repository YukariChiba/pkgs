pkgname=(patch)
pkgver=2.7.6
pkgrel=1
pkgdesc='A utility for patching difference listings against one or more original files'
arch=(x86_64)
url='http://savannah.gnu.org/projects/patch/'
license=(GPL3)
groups=(build-base)
depends=()
makedepends=()
options=()

source=(
    "http://ftp.gnu.org/gnu/patch/patch-${pkgver}.tar.xz"
)

sha256sums=(
    ac610bda97abe0d9f6b7c963255a11dcb196c25e337c61f94e4778d632f1d8fd
)


build() {
    cd_unpacked_src
    LDFLAGS='-static -Wl,-static' ./configure --prefix=/usr
    make V=1
}

package() {
    cd_unpacked_src
    make DESTDIR="${pkgdir}" install
    rm -rf "${pkgdir:?}/usr/lib"
}
