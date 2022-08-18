pkgname=gptfdisk
pkgver=1.0.8
pkgrel=1
pkgdesc='A set of text-mode partitioning tools'
arch=(x86_64)
url='http://www.rodsbooks.com/gdisk'
license=(GPL2)
groups=()
depends=()
makedepends=(
    libncurses-dev
    libuuid-dev
    popt-dev
)
options=()

source=(
    "http://www.rodsbooks.com/gdisk/${pkgname}-${pkgver}.tar.gz"
)

sha256sums=(
    95d19856f004dabc4b8c342b2612e8d0a9eebdd52004297188369f152e9dc6df
)


build() {
    cd_unpacked_src
    CXX=c++ CXXFLAGS+=' -static' \
        LDFLAGS='-static -Wl,-static -lunwind -lc++abi' MAKEFLAGS='' make
}

package() {
    cd_unpacked_src
    install -d "${pkgdir}/usr/sbin" "${pkgdir}/usr/share/man/man8"
    for bin in cgdisk gdisk sgdisk fixparts ; do
        install -m0755 $bin "${pkgdir}/usr/sbin/"
        install -m0644 "${bin}.8" "${pkgdir}/usr/share/man/man8/"
    done
}
