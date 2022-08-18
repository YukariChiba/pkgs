pkgname=(python python-dev)
_vermajor=3
_verminor=9
pkgver=${_vermajor}.${_verminor}.7
pkgrel=1
pkgdesc='A clear and powerful object-oriented programming language,'
arch=(x86_64)
url='http://www.python.org'
license=(Python)
groups=()
depends=()
makedepends=(
    libffi-dev
    libncurses-dev
    openssl-dev
    libsqlite-dev
    liblzma-dev
    readline-dev
    zlib-dev
)
options=()


source=(
    "https://www.python.org/ftp/python/${pkgver}/Python-${pkgver}.tar.xz"
    python-fix-ctypes_util.patch
)
sha256sums=(
    f8145616e68c00041d1a6399b76387390388f8359581abc24432bb969b5e3c57
    db33506472cb9819acf03e8206323ed0aea3cb0ed537b047976dc613e9a34e4e
)


build() {
    cd_unpacked_src
    patch -Np1 -i "${srcdir}/python-fix-ctypes_util.patch"
    unset CFLAGS CXXFLAGS
    CC='cc -fPIC' CXX='c++ -fPIC' ./configure \
        --prefix=/usr \
        --sysconfdir=/etc \
        --with-system-ffi
    make
}

check() {
    cd_unpacked_src
    #make test
}

package_python() {
    depends=(
        "ld-musl-$(arch).so.1"
        libcrypto.so.1.1
        libffi.so.7
        libreadline.so.8
        libsqlite3.so.0
        libssl.so.1.1
    )
    pkgfiles=(
        usr/bin/pip
        "usr/bin/pip${_vermajor}"
        usr/bin/python
        "usr/bin/python${_vermajor}"
        "usr/bin/python${_vermajor}.${_verminor}"
        "usr/lib/python${_vermajor}.${_verminor}"
        "usr/include/python${_vermajor}.${_verminor}/pyconfig.h"
    )
    cd_unpacked_src
    make DESTDIR="${pkgdirbase}/dest" install
    cd "${pkgdirbase}/dest" || return 1
    rm -rf "usr/lib/${_vermajor}.${_verminor}/site-packages"
    ln -s "python${_vermajor}.${_verminor}" usr/bin/python
    ln -s "pip${_vermajor}" usr/bin/pip
    find . -name "*.pyc" -delete -o -name "*.pyo" -delete
    find . -name 'test' -type d -exec rm -rf '{}' + || true
    package_defined_files
    rm "${pkgdirbase}/dest/usr/include/python${_vermajor}.${_verminor}/pyconfig.h"
}

package_python-dev() {
    depends=(
        "python=${pkgver}"
    )
    pkgfiles=(
        usr/bin/py*-config
        usr/include
        usr/lib/libpython*.a
        usr/lib/pkgconfig
    )
    std_split_package
}
