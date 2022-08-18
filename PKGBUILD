pkgname=mksh
pkgver=R59c
pkgrel=1
pkgdesc='The MirBSD Korn Shell'
arch=(x86_64)
url='https://www.mirbsd.org/mksh.htm'
license=(BSD)
groups=(base)
depends=()
makedepends=()
options=()
source=(
    "https://github.com/MirBSD/mksh/archive/mksh-${pkgver}.tar.gz"
)

sha256sums=(
    'SKIP'
)


build() {
    cd_unpacked_src
    LDSTATIC='-static' sh ./Build.sh -r -j
}

package() {
    cd_unpacked_src
    install -d "${pkgdir}/bin"
    install -d "${pkgdir}/usr/share/man/man1"
    install -m 0755 mksh "${pkgdir}/bin/"
    #install -c -o root -g bin -m 444 lksh.1 mksh.1 "${pkgdir}/usr/share/man/man1/"
    # Not available in chroot
    install -m 444 lksh.1 mksh.1 "${pkgdir}/usr/share/man/man1/"
}
