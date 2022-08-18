pkgname=busybox
pkgver=1.33.1
pkgrel=1
pkgdesc='Tiny versions of common UNIX utilities built into a single binary'
arch=(x86_64)
url='http://busybox.net'
license=(GPL)
groups=(base)
depends=()
makedepends=(
    skalibs-dev
    utmps-dev
)
options=(emptydirs)
source=(
    "http://busybox.net/downloads/${pkgname}-${pkgver}.tar.bz2"
    non-const.patch
    poweroff.patch
    busybox-config
    udhcpc.script
    sysctl.conf
    ntpd-service
    ntpd-log
    ntp.conf
    if-pre-up-bridge
    if-post-down-bridge
    syslogd-service
    syslogd-log
    klogd-service
    mkinitramfs
    initramfs-init
)

sha256sums=(
    'SKIP'
    'SKIP'
    'SKIP'
    'SKIP'
    'SKIP'
    'SKIP'
    'SKIP'
    'SKIP'
    'SKIP'
    'SKIP'
    'SKIP'
    'SKIP'
    'SKIP'
    'SKIP'
    'SKIP'
    'SKIP'
)

backup=(
    etc/ntp.conf
    etc/sysctl.conf
)


build() {
    cd_unpacked_src
    patch -Np1 -i "${srcdir}/non-const.patch"
    patch -Np1 -i "${srcdir}/poweroff.patch"
    sed "/CONFIG_PREFIX/s@=.*@=\"${pkgdir}/\"@" \
      "${srcdir}/busybox-config" >.config
    # shellcheck disable=SC2016
    sed -i -e 's@<none>@-lutmps -lskarnet@' \
        -e '/^l_list=/s@$LDLIBS@-lutmps -lskarnet@' \
        scripts/trylink
    make CFLAGS="$CFLAGS -static" \
        LDLIBS='-lutmps -lskarnet' \
        HOSTCC=clang CC=clang
}

package() {
    cd_unpacked_src
    make CFLAGS="$CFLAGS -static" \
        LDLIBS='-lutmps -lskarnet' \
        HOSTCC=clang CC=clang install
    cd "$pkgdir" || return 1

    # Setuid
    chmod u+s bin/busybox

    install -d usr/share/man/man1
    install -m0644 "${srcdir}/${pkgname}-${pkgver}/docs/busybox.1" usr/share/man/man1/

    # configuration/scripts
    install -d etc/network/if-pre-up.d
    install -m 0755 "${srcdir}/if-pre-up-bridge" \
        etc/network/if-pre-up.d/01-bridge
    install -d etc/network/if-up.d
    install -d etc/network/if-down.d
    install -d etc/network/if-post-down.d
    install -m 0755 "${srcdir}/if-post-down-bridge" \
        etc/network/if-post-down.d/01-bridge
    install -d usr/share/udhcpc
    install -m 0755 "${srcdir}/udhcpc.script" \
        usr/share/udhcpc/default.script
    install -m 0644 "${srcdir}/sysctl.conf" etc/
    install -m 0644 "${srcdir}/ntp.conf" etc/ntp.conf
    install -d sbin usr/bin usr/share/mkinitramfs
    ln -s /bin/busybox usr/bin/env
    ln -s /bin/busybox usr/bin/awk
    install -m 0755 "${srcdir}/mkinitramfs" usr/bin/
    install -m 0644 "${srcdir}/initramfs-init" usr/share/mkinitramfs/init.in

    # s6 Services
    install -d etc/s6/services/available/ntpd/log
    install -m 0754 "${srcdir}/ntpd-service" etc/s6/services/available/ntpd/run
    install -m 0754 "${srcdir}/ntpd-log" etc/s6/services/available/ntpd/log/run
    install -d etc/s6/services/available/syslogd/log
    install -m 0754 "${srcdir}/syslogd-service" etc/s6/services/available/syslogd/run
    install -m 0754 "${srcdir}/syslogd-log" etc/s6/services/available/syslogd/log/run
    install -d etc/s6/services/available/klogd
    install -m 0754 "${srcdir}/klogd-service" etc/s6/services/available/klogd/run
}
