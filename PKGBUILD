# Maintainer: Unmellow <amazingminecrafter2015 at gmail dot com>
# shellcheck shell=bash disable=SC2034,SC2154
#
# Fork of ~julienxx/asuka with Cursive 0.21 / crossterm (no ncurses).
# AUR/asuka (vladimyr) is still the upstream 0.8.5 ncurses tarball.
# This is the -git variant already published as asuka-git.
#
# Rust: extra/cargo + RUSTUP_TOOLCHAIN=stable (wiki Rust package guidelines).
# openssl-sys links the system library; do not vendor OpenSSL.

_pkgname=asuka
pkgname=asuka-git
pkgver=0.9.0.r0.g3796f0f
pkgrel=1
pkgdesc="Gemini Project client written in Rust with Cursive/crossterm"
arch=('x86_64')
url="https://github.com/unmellow/asuka"
license=('MIT')
depends=('gcc-libs' 'openssl')
makedepends=('cargo' 'git')
provides=("asuka=${pkgver}")
conflicts=('asuka')
options=('!lto')
source=("${_pkgname}::git+${url}.git")
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
