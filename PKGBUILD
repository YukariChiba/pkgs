pkgname=(mdevd)
pkgver=0.1.4.0
pkgrel=1
pkgdesc='A small daemon managing kernel hotplug events, similarly to udevd.'
arch=(x86_64)
url='http://skarnet.org/software/mdevd/'
license=(ISC)
groups=(base)
depends=(s6 execline)
makedepends=(skalibs-dev)
options=()

source=(
    "http://skarnet.org/software/mdevd/mdevd-${pkgver}.tar.gz"
    mdevd-service
    mdevd.install
    mdev.conf
    catch-all
    dev-bus-usb
    settle-nics
    sound-control
    storage-device
)

install=mdevd.install

sha256sums=(
    ffd3b223b4cf0e51253b4a8f09cb88d70bf22693228ab0818af174a3f099dcd2
    f44446d1dbae8308685e8ee016edde75016a4fd134398c468ad154fcb07a6e99
    c5ec938fe81c88d7e8dafc16a531d943f5f090659374e44cbba422f503fbcd30
    2578b47b0f48bab221f138d8280ca1ce7e5384b26d353ab4f5fd7e922581e0ac
    f9d22d7f00522076c421a2c39c48057e799409c799e825b7e177237eac3723b3
    0273c88a88eb057dabc6fe59ed563c5ad8e0eb8d39ef36f56f3484f4bfa8f959
    a55b5b27b2773c5442667e7db4e46ce131b67c78688c73f123e8531dc2384212
    4592e04a9b0d8f8492f351d305b43057e302163dbf25cc255e618fafd4ad5bc3
    b5d2b3b66ac683fc8b17dabf8fada623541441c0131241d56b0066d24933b568
)

backup=(etc/mdev.conf)

build() {
    cd_unpacked_src
    ./configure \
      --prefix=/ \
      --bindir=/sbin \
      --enable-static-libc
    make
}

package() {
    pkgfiles=(
        sbin
    )
    std_package
    install -d "${pkgdir}/etc" "${pkgdir}/lib/mdev/helpers"
    install -m0644 "${srcdir}/mdev.conf" "${pkgdir}/etc/mdev.conf"
    install -m0754 "${srcdir}/catch-all"      "${pkgdir}/lib/mdev/helpers/"
    install -m0754 "${srcdir}/dev-bus-usb"    "${pkgdir}/lib/mdev/helpers/"
    install -m0754 "${srcdir}/settle-nics"    "${pkgdir}/lib/mdev/helpers/"
    install -m0754 "${srcdir}/sound-control"  "${pkgdir}/lib/mdev/helpers/"
    install -m0754 "${srcdir}/storage-device" "${pkgdir}/lib/mdev/helpers/"

    # mdevd service
    install -d "${pkgdir}/etc/s6/init-services/mdevd"
    install -m 0754 "${srcdir}/mdevd-service" "${pkgdir}/etc/s6/init-services/mdevd/run"
    echo 3 >"${pkgdir}/etc/s6/init-services/mdevd/notification-fd"
}
