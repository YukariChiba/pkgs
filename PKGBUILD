pkgname=vim
_vermajor=8
_verminor=2
_verpatch=3388
pkgver="${_vermajor}.${_verminor}.${_verpatch}"
pkgrel=1
pkgdesc='An IMproved version of the vi editor'
arch=(x86_64)
url='http://www.vim.org'
license=(VIM)
groups=()
depends=()
makedepends=(libncurses-dev)
options=()

source=(
    "https://github.com/vim/vim/archive/v${pkgver}.tar.gz"
    vimrc
)

sha256sums=(
    0e1c04d25cb36f4cf3fdcd85d6b2a7df6923ea09551ed823e7adfba7bf19c6c1
    5e698ff1872bae79b7eae3f35bfca2e426c2698a785687fb9035e0fee16de91a
)


build() {
    cd_unpacked_src

    # Set the path of the default vimrc file
    echo '#define SYS_VIMRC_FILE "/etc/vimrc"' >> src/feature.h

    # Fix some feature tests
    sed -i -e '/thisterminaldoesnotexist/i #include <term.h>' \
           -e '/0xffffffffUL;/i #include <stdlib.h>' \
	   src/auto/configure

    CC='cc -I/include/ncursesw' \
        CFLAGS+=' -static -fPIC' LDFLAGS='-static -Wl,-static' \
        ./configure \
        --prefix=/usr \
        --enable-multibyte \
        --with-tlib=ncursesw
    make
}

package_vim() {
    pkgfiles=(
        usr/bin
        etc
        usr/share/man/man1
        usr/share/vim
    )
    options+=(emptydirs)
    cd_unpacked_src
    make DESTDIR="${pkgdirbase}/dest" install
    cd "${pkgdirbase}/dest" || return 1
    install -d etc
    install -m 0644 "${srcdir}/vimrc" etc/vimrc
    rm -f usr/bin/xxd
    package_defined_files
}
