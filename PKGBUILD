pkgname=(file file-dev)
pkgver=5.40
pkgrel=1
pkgdesc='A file-type guesser'
arch=(x86_64)
url='http://darwinsys.com/file/'
license=(BSD)
groups=()
depends=()
makedepends=()
options=()

source=(
    "ftp://ftp.astron.com/pub/file/file-${pkgver}.tar.gz"
)

sha256sums=(
    167321f43c148a553f68a0ea7f579821ef3b11c27b8cbe158e4df897e4a5dd57
)


build() {
    cd_unpacked_src
    sed -i 's/misc/file/' configure
    LDFLAGS='-Wl,-static' ./configure --prefix=/usr \
      --disable-shared \
      --enable-static
    make V=1
}

package_file() {
    options=()
    pkgfiles=(
        usr/bin/file
        usr/share/file/magic.mgc
    )
    std_package
}

package_file-dev() {
    pkgfiles=(
        usr/include
        usr/lib
    )
    std_split_package
}
