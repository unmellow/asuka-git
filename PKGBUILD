# Maintainer: Unmellow <name2020@googlemail.commerce>
_pkgname=asuka
pkgname=asuka-git
pkgver=r47.1c6d9ad
pkgrel=2
pkgdesc="a Gemini Project client written in Rust with NCurses."
arch=("x86_64" "i686")
url="https://git.sr.ht/~julienxx/asuka"
license=('custom:MIT')
depends=('ncurses' 'openssl')
makedepends=('git' 'rust')
provides=("$_pkgname")
conflicts=("$_pkgname")
source=('git+https://git.sr.ht/~julienxx/asuka')
sha512sums=('SKIP')

pkgver() {
  cd $_pkgname
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  cd $_pkgname
  cargo build --release
}

package() {
  cd $_pkgname
  install -Dm755 "./target/release/${_pkgname}" -t "${pkgdir}/usr/bin"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}