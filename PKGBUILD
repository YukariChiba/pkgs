pkgname='binutils'
rationale='This is part of the core toolchain'
pkgver=2.37
pkgrel=1
pkgdesc='A collection of binary tools, including a linker and an assembler'
arch=(x86_64)
url='http://www.gnu.org/software/binutils/'
license=(GPL3)
groups=()
depends=()
makedepends=(zlib-dev binutils)
options=()

source=(
    "http://ftp.gnu.org/gnu/binutils/binutils-${pkgver}.tar.xz"
)

sha256sums=(
    820d9724f020a3e69cb337893a0b63c2db161dadcb0e06fc11dc29eb1e84a32c
)

build() {
    cd_unpacked_src
    mkdir build
    cd build || return 1
    export PATH=/opt/binutils/bin:$PATH
    ../configure --prefix=/usr \
      --build="$CHOST" \
      --host="$CHOST" \
      --target="$CHOST" \
      --enable-64-bit-bfd \
      --disable-plugins \
      --disable-shared \
      --disable-werror \
      --disable-nls \
      --with-system-zlib
    make tooldir=/usr
}

package() {
    depends=(
        "ld-musl-$(arch).so.1"
    )
    cd_unpacked_src
    cd build || return 1
    make prefix="$pkgdir/usr" tooldir="$pkgdir/usr" install
    rm -rf "${pkgdir:?}/info"
}

