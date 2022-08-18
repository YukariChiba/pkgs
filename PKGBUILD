pkgname=(openssh-client)
_vermajor=8
_verminor=7
pkgver=${_vermajor}.${_verminor}p1
pkgrel=1
pkgdesc='the premier connectivity tool for remote login with the SSH protocol'
arch=(x86_64)
url='https://openssh.com'
license=(BSD)
groups=()
depends=()
makedepends=(
    openssl-dev
    zlib-dev
)
options=()


source=(
    "https://ftp4.usa.openbsd.org/pub/OpenBSD/OpenSSH/portable/openssh-${pkgver}.tar.gz"
)
sha256sums=(
    7ca34b8bb24ae9e50f33792b7091b3841d7e1b440ff57bc9fabddf01e2ed1e24
)


build() {
    cd_unpacked_src
    export LDFLAGS='-static -Wl,-static'
    ./configure \
        --prefix=/usr \
        --sysconfdir=/etc \
        --with-mantype=man
    make
}

package_openssh-client() {
    depends=(
    )
    pkgfiles=(
        usr/bin/ssh
        usr/bin/ssh-keyscan
        usr/bin/ssh-keygen
        usr/bin/scp
        usr/bin/sftp
        usr/bin/ssh
        usr/bin/ssh-agent
        usr/bin/ssh-add
        etc/ssh_config
        usr/share/man/man1
    )
    std_package
}
