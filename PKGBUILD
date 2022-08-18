rationale='Pacman primarily uses libcurl for downloading files'
pkgname=(
    curl
    libcurl
    libcurl-dev
    ca-certs
)
pkgver=7.79.0
pkgrel=1
pkgdesc='An API for writing text-based user interfaces'
arch=(x86_64)
url='http://curl.se'
license=(GPL2)
groups=()
depends=()
makedepends=(openssl-dev perl zlib-dev)
options=()


source=(
    "${url}/download/${pkgname[0]}-${pkgver}.tar.bz2"
)
sha256sums=(
    d607a677f473f79f96c964100327125a6204a39d835dc00dab7fc0129b959f42
)

build() {
    cd_unpacked_src
    rm src/tool_hugehelp.c
    CFLAGS+=' -fPIC' LDFLAGS='--static' \
    ./configure \
      --prefix=/usr \
      --enable-static \
      --disable-shared \
      --with-ssl \
      --with-ca-bundle=/etc/ssl/certs/ca-certificates.crt
    make V=1
    install -v src/curl{,-static}
    unset LDFLAGS
    make clean
    CFLAGS+=' -fPIC' \
    ./configure \
      --prefix=/usr \
      --enable-static \
      --enable-shared \
      --with-ssl \
      --with-ca-bundle=/etc/ssl/certs/ca-certificates.crt
    make V=1
}

package_curl() {
    pkgfiles=(
        usr/bin/curl
    )
    depends=(
        ca-certs
    )
    cd_unpacked_src
    make DESTDIR="${pkgdirbase}/dest" install
    install -m0755 -v src/curl-static "${pkgdirbase}/dest/usr/bin/curl"
    std_split_package
}

package_libcurl() {
    pkgfiles=(
        usr/lib/libcurl.so.*
    )
    depends=(
        ca-certs
        "ld-musl-$(arch).so.1"
        libssl.so.1.1
        libcrypto.so.1.1
    )
    provides=(
        libcurl.so.4
    )
    std_split_package
}

package_libcurl-dev() {
    pkgfiles=(
        usr/bin/curl-config
        usr/include
        usr/lib/*.a
        usr/lib/*.so
        usr/lib/pkgconfig
        usr/share/aclocal
    )
    depends=(
        "libcurl=${pkgver}"
    )
    std_split_package
}

package_ca-certs() {
    cd_unpacked_src
    ./lib/mk-ca-bundle.pl
    install -d "${pkgdir}/etc/ssl/certs"
    install -m0644 ca-bundle.crt "${pkgdir}/etc/ssl/certs/ca-certificates.crt"
    ln -s certs/ca-certificates.crt "${pkgdir}/etc/ssl/cert.pem"
    ln -s certs/ca-certificates.crt "${pkgdir}/etc/ssl/ca-certs.pem"
}
