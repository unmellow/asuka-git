# Maintainer: Unmellow <amazingminecrafter2015 at gmail dot com>
# shellcheck shell=bash disable=SC2034,SC2154
#
# AUR/asuka (vladimyr) is the 0.8.5 release tarball. This is the -git
# variant already published as asuka-git. Both may coexist.
#
# Rust: extra/cargo + RUSTUP_TOOLCHAIN=stable (wiki Rust package guidelines).
# That replaces the old rustup-default-toolchain echo. openssl-sys and
# ncurses-sys link the system libraries; do not vendor OpenSSL.

_pkgname=asuka
pkgname=asuka-git
pkgver=0.8.5.r0.gc23cf82
pkgrel=1
pkgdesc="Gemini Project client written in Rust with NCurses"
arch=('x86_64')
url="https://git.sr.ht/~julienxx/asuka"
license=('MIT')
depends=('gcc-libs' 'ncurses' 'openssl')
makedepends=('cargo' 'git')
provides=("asuka=${pkgver}")
conflicts=('asuka')
options=('!lto')
source=("${_pkgname}::git+${url}")
sha256sums=('SKIP')

pkgver() {
  cd "${_pkgname}"
  git describe --long --tags --abbrev=7 | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd "${_pkgname}"
  export RUSTUP_TOOLCHAIN=stable
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "${_pkgname}"
  export RUSTUP_TOOLCHAIN=stable
  export CARGO_TARGET_DIR=target
  export OPENSSL_NO_VENDOR=1
  cargo build --frozen --release
}

package() {
  cd "${_pkgname}"
  install -Dm755 "target/release/${_pkgname}" "${pkgdir}/usr/bin/${_pkgname}"
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
