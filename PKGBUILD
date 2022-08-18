pkgname=dropbear
pkgver=2020.81
pkgrel=1
pkgdesc='A relatively small SSH server and client.'
arch=(x86_64)
url='http://matt.ucc.asn.au/dropbear/dropbear.html'
license=(MIT)
groups=()
depends=(s6 execline)
makedepends=(
    skalibs-dev
    utmps-dev
    zlib-dev
)
options=()

source=(
    "http://matt.ucc.asn.au/dropbear/releases/dropbear-${pkgver}.tar.bz2"
    dropbear-service
    dropbear-log
    dropbear-finish
    dropbear.install
)

sha256sums=(
    48235d10b37775dbda59341ac0c4b239b82ad6318c31568b985730c788aac53b
    cd91a5635e4cf9564691b34c082e1371a2001b783ded3ea5c1fdf5629fb44eae
    992a38e175c6dd8dea0c0496dbe175749f0f18eee6d861d913cd8f5bfe19a37a
    678981da5f219b6d335e132073ce5516e51470f80d17f33b282af259d846c5b0
    0d6cbdcf92e9c0d3793970f5a068673e8d53ab42c958aaa7920a683699e909cd
)

install=dropbear.install

build() {
    cd_unpacked_src
    sed -i '/MAX_CMD_LEN/s@9000@20000@' sysoptions.h
    LIBS='-lutmps -lskarnet' \
        ./configure \
            --prefix=/usr \
            --disable-utmp \
            --disable-wtmp \
            --enable-utmpx \
            --enable-wtmpx \
            --enable-static
    make PROGRAMS="dropbear dbclient dropbearkey dropbearconvert scp"
}

package() {
    options+=(emptydirs)
    cd_unpacked_src
    make DESTDIR="$pkgdir" \
      PROGRAMS="dropbear dbclient dropbearkey dropbearconvert scp" \
      install
    mv "${pkgdir}/usr/bin/scp" "${pkgdir}/usr/bin/dropbear-scp"
    install -d -m 0755 "${pkgdir}/etc/dropbear"
    install -d "${pkgdir}/etc/s6/services/available/dropbear/log"
    install -m 0754 "${srcdir}/dropbear-service" \
        "${pkgdir}/etc/s6/services/available/dropbear/run"
    install -m 0754 "${srcdir}/dropbear-finish" \
        "${pkgdir}/etc/s6/services/available/dropbear/finish"
    install -m 0754 "${srcdir}/dropbear-log" \
        "${pkgdir}/etc/s6/services/available/dropbear/log/run"
    rm -rf "$pkgdir"/share
}
