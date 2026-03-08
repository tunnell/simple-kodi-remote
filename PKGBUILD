# Maintainer: tunnell
pkgname=skr
pkgver=1.0.0
pkgrel=1
pkgdesc="Simple Kodi Remote - A terminal-based remote control for Kodi"
arch=('any')
url="https://github.com/tunnell/simple-kodi-remote"
license=('GPL3')
depends=('zsh' 'kodi-eventclients' 'ncurses')
source=("skr" "LICENSE.md")
sha256sums=('26ca3c29b213fbd6befe1a526a104d9fe5af9763004506ccdbafff37daf165ec'
            'cc5470feed66192387f06ae93aed0bd4fefae5a5fd7c1e54a4acf4ea64f1028b')

package() {
    install -Dm755 "$srcdir/skr" "$pkgdir/usr/bin/skr"
    install -Dm644 "$srcdir/LICENSE.md" "$pkgdir/usr/share/licenses/$pkgname/LICENSE.md"
}
