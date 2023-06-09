# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Dag Odenhall <dag.odenhall@gmail.com>
# Contributor: Grigorios Bouzakis <grbzks@gmail.com>

pkgname=dwm
pkgver=6.4
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="https://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2' 'st' 'dmenu')
install=dwm.install
source=(dwm.desktop
        https://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
        https://dwm.suckless.org/patches/systray/dwm-systray-6.4.diff
        https://dwm.suckless.org/patches/alt-tab/dwm-alttab-6.4.diff
        config.h)
sha256sums=('bc36426772e1471d6dd8c8aed91f288e16949e3463a9933fee6390ee0ccd3f81'
            'fa9c0d69a584485076cfc18809fd705e5c2080dafb13d5e729a3646ca7703a6e'
            'e5e205b9286b8b65821ee60fe8dc93bfd686c39cc6c07cdd82af52a824825d06'
            'SKIP'
            'SKIP')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"
  cp "$srcdir/config.h" config.h
  patch -p1 < $srcdir/dwm-systray-6.4.diff
  patch -p1 < $srcdir/dwm-alttab-6.4.diff
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
  install -Dm644 "$srcdir/dwm.desktop" "$pkgdir/usr/share/xsessions/dwm.desktop"
}
