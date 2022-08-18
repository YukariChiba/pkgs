pkgname=nginx
pkgver=1.21.1
pkgrel=1
pkgdesc='An HTTP and reverse proxy server.'
arch=(x86_64)
url='http://nginx.org/'
license=(BSD)
groups=()
depends=(s6 execline)
makedepends=(
    pkgconf
    libpcre-dev
    openssl-dev
    zlib-dev
)
options=(emptydirs)

source=(
    "http://nginx.org/download/nginx-${pkgver}.tar.gz"
    nginx-service
    nginx-log
    nginx.install
    nginx.conf
    99-default
)

sha256sums=(
    68ba0311342115163a0354cad34f90c05a7e8bf689dc498abf07899eda155560
    46d22dd25d7628a3696396f7d35352f7e6e0eb03369bb3c2dad000d23b3dee8b
    9b4f42034d0130d041dfc8f0fcc262891a7d12a529379c6ca344b4a898248d25
    9df79cf0c61958cc9d4d74ef7831d5d70c1c58bc859b36a2299c5853d66bb30a
    6446799214aa0856c2442bb8864b14c105991f2b96a98908d47db5710c6f896b
    4d3411f16e5c7bef5c0c2f9865ffbbbe2c226fa073ab7fd8a4e54547fff875f2
)

install=nginx.install


build() {
    cd_unpacked_src
    sed -i 's@-Wl,-E@-Wl,-static@g' auto/cc/conf
    CC='cc -static -fPIC' \
    ./configure \
        --prefix=/usr \
        --conf-path=/etc/nginx/nginx.conf \
        --pid-path=/var/run/nginx.pid \
        --lock-path=/var/lock/nginx.lock \
        --http-log-path=/proc/self/fd/1 \
        --error-log-path=/proc/self/fd/2 \
        --http-client-body-temp-path=/var/tmp/nginx/client_body \
        --http-proxy-temp-path=/var/tmp/nginx/proxy \
        --http-fastcgi-temp-path=/var/tmp/nginx/fastcgi \
        --http-uwsgi-temp-path=/var/tmp/nginx/uwsgi \
        --http-scgi-temp-path=/var/tmp/nginx/scgi \
        --user=nginx \
        --group=nogroup \
        --with-threads
    make
}

package() {
    pkgfiles=
    cd_unpacked_src
    make DESTDIR="$pkgdir" install

    # Share files
    install -d "${pkgdir}"/usr/share/nginx
    mv "${pkgdir}"/usr/html "${pkgdir}"/usr/share/nginx/

    # Configuration
    install -d "${pkgdir}/etc/nginx/conf.d"
    install -d "${pkgdir}/etc/nginx/sites-available"
    install -d "${pkgdir}/etc/nginx/sites-enabled"
    install -m 0644 "${srcdir}/99-default" "${pkgdir}/etc/nginx/sites-available/"
    install -m 0644 "${srcdir}/nginx.conf" "${pkgdir}/etc/nginx/"

    # Service files
    install -d "${pkgdir}/etc/s6/services/available/nginx/log"
    install -m 0754 "${srcdir}/nginx-service" \
        "${pkgdir}/etc/s6/services/available/nginx/run"
    install -m 0754 "${srcdir}/nginx-log" \
        "${pkgdir}/etc/s6/services/available/nginx/log/run"

    # Cleanup
    find "$pkgdir"/etc -name "*.default" -delete
    rm -rf "${pkgdir:?}/"{var,proc}
}
