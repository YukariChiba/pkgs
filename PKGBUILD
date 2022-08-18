rationale='libarchive is a core dependency of pacman'
pkgname=(
    libarchive
    libarchive-dev
)
pkgver=3.5.2
pkgrel=1
pkgdesc='Multi-format archive and compression library'
arch=(x86_64)
url='http://www.libarchive.org'
license=(BSD)
groups=()
depends=()
makedepends=(
    libacl-dev
    libattr-dev
    liblzma-dev
    zlib-dev
)
options=()

source=(
    "http://www.libarchive.org/downloads/libarchive-${pkgver}.tar.gz"
)
sha256sums=(
    5f245bd5176bc5f67428eb0aa497e09979264a153a074d35416521a5b8e86189
)


build() {
    cd_unpacked_src
    # fix for musl
    sed -i 's@HAVE_LCHMOD@&_DISABLE@' libarchive/archive_write_disk_posix.c
    # fixes for busybox xz
    sed -i 's@ -qq@@' libarchive/archive_read_support_filter_xz.c
    sed -i 's@xz -d@unxz@' libarchive/archive_read_support_filter_xz.c
    sed -i 's@lzma -d@unlzma@' libarchive/archive_read_support_filter_xz.c
    CFLAGS+=' -fPIC --static' LDFLAGS='-static -Wl,-static' \
        ./configure \
        --prefix=/usr \
        --disable-shared \
        --enable-static
    make V=1
}

package_libarchive() {
    pkgfiles=(
        usr/bin
        usr/share/man/man1
        usr/share/man/man5/libarchive-formats*
    )
    std_package
}

package_libarchive-dev() {
    depends=(libarchive)
    pkgfiles=(
        usr/include
        usr/lib/*.a
        usr/lib/pkgconfig
        usr/share/man/man3
    )
    depends=(libarchive)
    std_split_package
}
