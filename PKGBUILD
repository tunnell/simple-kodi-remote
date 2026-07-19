# Maintainer: tunnell
pkgname=skr
pkgver=1.0.0
pkgrel=1
pkgdesc="Simple Kodi Remote - hardened terminal remote for Kodi via kodi-send (no web server needed)"
arch=('any')
url="https://github.com/tunnell/simple-kodi-remote"
license=('GPL3')
depends=('zsh' 'kodi-eventclients' 'ncurses')
source=("$pkgname-$pkgver.tar.gz::https://github.com/tunnell/simple-kodi-remote/archive/v$pkgver.tar.gz")
sha256sums=('ca4967f33fafd3c3793121370b2159cc6e4d596cfa37f9d909adcdc0374fafee')

package() {
    cd "simple-kodi-remote-$pkgver"
    install -Dm755 skr "$pkgdir/usr/bin/skr"
    install -Dm644 LICENSE.md "$pkgdir/usr/share/licenses/$pkgname/LICENSE.md"
}
