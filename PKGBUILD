pkgname=ninja
pkgver=1.10.2
pkgrel=1
pkgdesc='a small build system with a focus on speed'
arch=(x86_64)
url='https://github.com/ninja-build/ninja'
license=(GPL2)
groups=()
depends=(python)
makedepends=()
options=()


source=(
    "https://github.com/ninja-build/ninja/archive/v${pkgver}.tar.gz"
)
sha256sums=(
    ce35865411f0490368a8fc383f29071de6690cbadc27704734978221f25e2bed
)


build() {
    cd_unpacked_src
    LDFLAGS='-static -Wl,-static -lc++abi -lunwind' ./configure.py --bootstrap
}

package() {
    cd_unpacked_src
    install -d "${pkgdir}/bin"
    install -m 0755 ninja "${pkgdir}/bin/"
}
