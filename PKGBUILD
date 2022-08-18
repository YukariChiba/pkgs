pkgname=iptables
pkgver=1.8.7
pkgrel=1
pkgdesc='A fast incremental file transfer utility'
arch=(x86_64)
url='http://www.netfilter.org/'
license=(GPL)
groups=()
depends=()
makedepends=(zlib-dev)
options=()

source=(
    "https://www.netfilter.org/projects/iptables/files/${pkgname}-${pkgver}.tar.bz2"
)

sha256sums=(
    c109c96bb04998cd44156622d36f8e04b140701ec60531a10668cfdff5e8d8f0
)


build() {
    cd_unpacked_src
    LDFLAGS='-static -Wl,-static' \
      ./configure --prefix='' \
      --disable-shared \
      --enable-static \
      --disable-nftables \
      --enable-libipq \
      --mandir=/usr/share/man \
      --with-xtlibdir=/lib/xtables
    make
}

package() {
    pkgfiles=(
        bin
        sbin
        usr/share/man/man1
        usr/share/man/man8
    )
    std_package
}
