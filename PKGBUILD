pkgname=gettext
pkgver=0.21
pkgrel=1
pkgdesc='A framework for producing multi-lingual messages.'
arch=(x86_64)
url='http://www.gnu.org/software/gettext'
license=(GPL3)
groups=()
depends=()
makedepends=()
options=()
changelog=ChangeLog
source=(
    "http://ftp.gnu.org/gnu/${pkgname}/${pkgname}-${pkgver}.tar.xz"
)

sha256sums=(
    d20fcbb537e02dcf1383197ba05bd0734ef7bf5db06bdb241eb69b7d16b73192
)

PURGE_TARGETS+=(usr/lib/charset.alias usr/include/libintl.h)

build() {
    cd_unpacked_src
    ./configure --prefix=/usr \
        --enable-static \
        --disable-shared
    make
}

package() {
    depends=(
        "ld-musl-$(arch).so.1"
    )
    cd_unpacked_src
    make DESTDIR="$pkgdir" install
    rm -rf "${pkgdir}/usr/share/"{doc,info}
}
