# Maintainer: LeonRein <LeonRein at protom dot me>
_pkgname=reboot-to-windows
pkgname=${_pkgname}-git
pkgver=r1.0.0
pkgrel=1
pkgdesc="A simple utility to reboot into Windows from Linux"
arch=('any')
url="https://github.com/LeonRein/reboot-to-windows"
license=('GPL3')
depends=('polkit')
makedepends=('git')
source=("git+$url.git")
sha256sums=('SKIP')
install=reboot-to-windows.install

pkgver() {
  cd "$srcdir/${_pkgname}"
  ( set -o pipefail
    git describe --long --tags --abbrev=7 2>/dev/null | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
  )
}

package() {
  cd "$srcdir/${_pkgname}"

  # Install main scripts
  install -Dm755 scripts/reboot-to-windows.sh "$pkgdir/usr/bin/reboot-to-windows"
  install -Dm755 scripts/reboot-to-windows-pkexec.sh "$pkgdir/usr/lib/reboot-to-windows-pkexec.sh"
  
  # Install desktop files
  install -Dm644 desktop/reboot-to-windows.root.desktop "$pkgdir/usr/share/applications/reboot-to-windows.desktop"
  
  # Install policy file as documentation only
  install -Dm644 polkit/wartybix.reboot-to-windows.policy "$pkgdir/usr/share/doc/$pkgname/action/wartybix.reboot-to-windows.policy"
  
  # Install polkit rule as documentation only
  install -Dm644 polkit/50-wartybix.reboot-to-windows.rules "$pkgdir/usr/share/doc/$pkgname/rules.d/50-wartybix.reboot-to-windows.rules"
  
  # Install icons
  install -Dm644 icons/reboot-to-windows.svg "$pkgdir/usr/share/icons/reboot-to-windows.svg"
  install -Dm644 icons/wartybix.RebootToWindows.Source.svg "$pkgdir/usr/share/icons/wartybix.RebootToWindows.Source.svg"
  
  # Install documentation
  install -Dm644 doc/LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 doc/README.md "$pkgdir/usr/share/doc/$pkgname/README.md"

}
