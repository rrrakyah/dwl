# Maintainer: Devin J. Pohly <djpohly+arch@gmail.com>
pkgname=dwl-kat
_gitname=dwl-patched
pkgver=r478.c6d839a
pkgrel=1
pkgdesc="Simple, hackable dynamic tiling Wayland compositor (dwm for Wayland)"
arch=('x86_64')
url="https://github.com/djpohly/dwl"
license=('GPL')
depends=('wlroots')
conflicts=(dwl)
source=(git+https://github.com/rrrakyah/dwl-patched
        config.h
       	dwl.desktop)
sha256sums=(SKIP #'ee03a2cac6c4477702c8014e5ae5455c0acf4f47b87441c06e5da545ec234fa1'
            SKIP
            SKIP)

pkgver() {
  cd "$_gitname"
  ( set -o pipefail
    git describe --long 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}

prepare() {
  cd "$srcdir/$_gitname"
  git checkout patched
  cp "$srcdir/config.h" config.h
}

build() {
	cd "$srcdir/$_gitname"
	make
}

package() {
	cd "$srcdir/$_gitname"
	make PREFIX="$pkgdir/usr/" install
	install -m644 -D "$srcdir/dwl.desktop" "$pkgdir/usr/share/wayland-sessions/dwl.desktop"
}
