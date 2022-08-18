pkgname=(go)
pkgver=1.17
pkgrel=1
pkgdesc='An expressive, concise, clean and efficient programming language'
arch=(x86_64)
url='https://golang.org'
license=(BSD)
groups=()
depends=()
makedepends=(go)
options=(!strip)


source=(
    "https://golang.org/dl/go${pkgver}.src.tar.gz"
)
sha256sums=(
    3a70e5055509f347c0fb831ca07a2bf3b531068f349b14a3c652e9b5b67beb5d
)


build() {
    cd "${srcdir}/go/src" || return 1
    GOROOT_FINAL=/usr/lib/go \
      GOROOT_BOOTSTRAP=/usr/lib/go \
      GO_LDFLAGS='-s -w -buildmode=pie'
      CC=clang \
      ./make.bash
}

check() {
    # Disable for now
    return 0
    cd "${srcdir}/go/src" || return 1
    # cgo detects musl by detecting alpine :(
    touch /etc/alpine-release
    PATH="${srcdir}/go/bin:$PATH" \
    GOROOT_FINAL=/lib/go \
      GOROOT_BOOTSTRAP=/lib/go \
      GO_LDFLAGS='-s -w -buildmode=pie'
      CC=clang \
      ./run.bash -no-rebuild
}

package_go() {
    pkgfiles=(
        usr/bin/go
        usr/bin/gofmt
        usr/lib/go/bin
        usr/lib/go/lib
        usr/lib/go/pkg
        usr/lib/go/src
    )
    depends=(
        ca-certs
        "ld-musl-$(arch).so.1"
    )

    install -d "${pkgdirbase}"/dest/usr/{bin,lib}
    cd "${srcdir}" || return 1
    cp -a go "${pkgdirbase}/dest/usr/lib/"
    cd "${pkgdirbase}/dest" || return 1
    find usr/lib/go/src -type f -name "*_test.go" -delete
    find usr/lib/go/src -type d -name testdata -exec rm -rf '{}' +
    find usr/lib/go/src -type f \( -name "*.bash" -o -name "*.rc" -o -name "*.bat" \) -delete
    rm -rf usr/lib/go/pkg/bootstrap
    rm -rf usr/lib/go/pkg/tool/*/api
    rm -rf usr/lib/go/pkg/obj
    ln -s /usr/lib/go/bin/go usr/bin/go
    ln -s /lib/go/bin/gofmt usr/bin/gofmt
    package_defined_files
}
