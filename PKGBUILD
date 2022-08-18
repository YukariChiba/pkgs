pkgname=(utmps utmps-dev)
pkgver=0.1.0.2
pkgrel=1
pkgdesc='An implementation of the utmpx.h family of functions performing user accounting'
arch=(x86_64)
url='http://skarnet.org/software/utmps/'
license=(ISC)
groups=()
depends=(s6)
makedepends=(skalibs-dev)
options=()

source=(
    "http://skarnet.org/software/utmps/utmps-${pkgver}.tar.gz"
    utmpd-service
    wtmpd-service
    utmps.install
)

sha256sums=(
    8b6e0a0504bd8082e280c9823d67af2c694dc79a866c0d302938fe62ea515fee
    9b0f7494428bd28616ba5cbb98ac7c7b33ebbba89a8f0faa646aec15a155946f
    883916402e92f92c9f239f753c13fc362d0047fb797b3a2d82e4f6b2610a1368
    0ed97caa2758d0b93b0d9eb6b6efc6f613b0237af8ef2df45ac8d211a072b968
)

install=utmps.install


build() {
    cd_unpacked_src
    ./configure \
        --prefix=/usr \
        --bindir=/sbin \
        --libdir=/usr/lib \
        --with-sysdeps=/lib/skalibs/sysdeps \
        --enable-libc-includes \
        --enable-static-libc
    make
}

package_utmps() {
    groups=(base)
    pkgfiles=(
        sbin
    )
    std_package
    install -d "${pkgdir}/etc/s6/init-services/utmpd"
    install -m 0754 "${srcdir}/utmpd-service" "${pkgdir}/etc/s6/init-services/utmpd/run"
    echo 3 >"${pkgdir}/etc/s6/init-services/utmpd/notification-fd"
    install -d "${pkgdir}/etc/s6/init-services/wtmpd"
    install -m 0754 "${srcdir}/wtmpd-service" "${pkgdir}/etc/s6/init-services/wtmpd/run"
    echo 3 >"${pkgdir}/etc/s6/init-services/wtmpd/notification-fd"
}

package_utmps-dev() {
    pkgfiles=(
        usr/include
        usr/lib
    )
    std_split_package
}
