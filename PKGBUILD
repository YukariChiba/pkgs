pkgname=(pacman pacman-build)
pkgver=6.0.1
pkgrel=1
pkgdesc='A lightweight Package Manager'
arch=(x86_64)
url='https://www.archlinux.org/pacman/'
license=(GPL2)
groups=()
depends=()
makedepends=(
    libacl-dev
    libarchive-dev
    libcurl-dev
    liblzma-dev
    ninja
    openssl-dev
    perl
    pkgconf
    python
    zlib-dev
)
options=()

source=(
    "https://sources.archlinux.org/other/pacman/pacman-${pkgver}.tar.xz"
    static-build.patch
    makepkg.conf
    pacman.conf
    fakeroot
    dependencies.sh
    zz-dedup.sh
    std-build-functions.sh
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
)

build() {
    pip install meson
    export PATH=~/.local/bin:$PATH

    cd_unpacked_src
    sed -i -e 's/EUID == 0/EUID == -1/' scripts/makepkg.sh.in
    sed -i '/bsdtar -xf .*dbfile/s@-C@--no-fflags -C@' scripts/repo-add.sh.in
    patch -Np1 -i "${srcdir}/static-build.patch"
    export CFLAGS+=' -static'

    mkdir build
    cd build || return
    meson --prefix=/usr -Dbuildstatic=true ..
    ninja --verbose
}

package_pacman() {
    backup=(etc/pacman.conf)
    pkgfiles=(
        usr/bin/pacman
        usr/bin/pacman-conf
        usr/bin/pacman-db-upgrade
        usr/bin/vercmp
        etc/pacman.conf*
        var
    )
    groups=(base)

    cd_unpacked_src
    cd build || return
    DESTDIR="${pkgdirbase}/dest" meson install
    cd "${pkgdirbase}/dest" || return 1
    mv etc/pacman.conf{,.example}
    mv etc/makepkg.conf{,.example}
    install -m 0644 "${srcdir}/pacman.conf" etc/
    install -m 0644 "${srcdir}/makepkg.conf" etc/
    install -m 0755 "${srcdir}/fakeroot" usr/bin/
    install -m 0755 "${srcdir}/dependencies.sh" usr/share/makepkg/lint_package/
    # Named zz-dedup.sh because it needs to be executed last in the tidy stage
    install -m 0755 "${srcdir}/zz-dedup.sh" usr/share/makepkg/tidy/
    install -m 0755 "${srcdir}/std-build-functions.sh" usr/share/makepkg/
    package_defined_files
}

package_pacman-build() {
    backup=(etc/makepkg.conf)
    pkgfiles=(
        usr/bin/fakeroot
        usr/bin/makepkg
        usr/bin/makepkg-template
        usr/bin/repo-*
        usr/bin/testpkg
        etc/makepkg.conf*
        usr/share
    )
    depends=(
        bash
        curl
        fedup
        file
        libarchive
        "pacman=${pkgver}"
        xz
    )
    std_split_package
}
