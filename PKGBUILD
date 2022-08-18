pkgname=autoconf
rationale="Many source packages ship with pre-generated build scripts. \
Pacman does not. Autoconf, automake and libtool are required to generate \
them before using."
pkgver=2.71
pkgrel=1
pkgdesc='A tool that produces shell scripts to automatically configure source code.'
arch=(x86_64)
url='http://www.gnu.org/software/autoconf'
license=(GPL3)
groups=()
depends=(perl)
makedepends=()
options=()

source=(
	"http://ftp.gnu.org/gnu/${pkgname}/${pkgname}-${pkgver}.tar.xz"
)

sha256sums=(
    f14c83cfebcc9427f2c3cea7258bd90df972d92eb26752da4ddad81c87a0faa4
)


build() {
    std_build
}

package() {
    cd_unpacked_src
    make DESTDIR="$pkgdir" install
    rm -rf "${pkgdir:?}/usr/share/"{info,doc}
}
