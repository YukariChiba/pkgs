pkgname=fedup
pkgver=1.0.0
pkgrel=1
pkgdesc='A simple File dEDUPlicator'
arch=(x86_64)
url='https://github.com/jhuntwork/fedup'
license=(MIT)
groups=()
depends=()
makedepends=()
options=()


source=(
    "https://github.com/jhuntwork/fedup/releases/download/v${pkgver}/fedup_${pkgver}_linux_amd64.tar.gz"
)
sha256sums=(
    df414ba1b44496f2448a16d7d657205581a5673e7725468b8651b3f8082ebc04
)


build() {
    cd_unpacked_src
}

package() {
    cd_unpacked_src
    install -d "${pkgdir}/bin"
    install -m 0755 fedup "${pkgdir}/bin/"
}
