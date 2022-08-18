pkgname=rsync
pkgver=3.2.3
pkgrel=1
pkgdesc='A fast incremental file transfer utility'
arch=(x86_64)
url='https://rsync.samba.org/'
license=(GPL3)
groups=()
depends=()
makedepends=(zlib-dev perl)
options=()

source=(
    "https://download.samba.org/pub/rsync/src/rsync-${pkgver}.tar.gz"
)

sha256sums=(
    becc3c504ceea499f4167a260040ccf4d9f2ef9499ad5683c179a697146ce50e
)


build() {
    cd_unpacked_src
    LDFLAGS='-static -Wl,-static' \
      ./configure --prefix=/usr \
        --disable-openssl \
        --disable-xxhash \
        --disable-zstd \
        --disable-lz4
    make
}

package() {
    pkgfiles=(
        usr/bin/rsync
        usr/share/man/man1
    )
    std_package
}
