pkgname=(bison bison-dev)
pkgver=3.7.6
pkgrel=1
pkgdesc='A general-purpose parser generator.'
arch=('x86_64')
url='http://www.gnu.org/software/bison/'
license=('GPL3')
groups=()
depends=()
makedepends=(flex perl)
options=()

source=(
    "http://ftp.gnu.org/gnu/${pkgname[0]}/${pkgname[0]}-$pkgver.tar.xz"
)

sha256sums=(
    67d68ce1e22192050525643fc0a7a22297576682bef6a5c51446903f5aeef3cf
)

build() {
    std_build
}

check() {
    cd_unpacked_src
    make check
}

package_bison() {
    pkgfiles=(
        usr/bin/bison
        usr/bin/yacc
        usr/share/bison
        usr/share/man/man1/bison.1
        usr/share/man/man1/yacc.1
        usr/share/aclocal/bison-i18n.m4
    )
    depends=(
        m4
        "ld-musl-$(arch).so.1"
    )
    std_package
}

package_bison-dev() {
    pkgfiles=(
        usr/lib/liby.a
    )
    std_split_package
}
