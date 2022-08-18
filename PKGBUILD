pkgname=automake
rationale="Many source packages ship with pre-generated build scripts. \
Pacman does not. Autoconf, automake and libtool are required to generate them \
before using."
pkgver=1.16.4
pkgrel=1
pkgdesc='A tool for automatically generating Makefile.in files.'
arch=(x86_64)
url='http://www.gnu.org/software/automake'
license=(GPL3)
groups=()
depends=(autoconf)
makedepends=()
options=()

source=(
	"http://ftp.gnu.org/gnu/${pkgname}/${pkgname}-${pkgver}.tar.xz"
)

sha256sums=(
    80facc09885a57e6d49d06972c0ae1089c5fa8f4d4c7cfe5baea58e5085f136d
)


build() {
    std_build
}

package() {
    pkgfiles=(
        usr/bin
        usr/share/aclocal-*
        usr/share/automake-*
        usr/share/man
    )
    std_package
}
