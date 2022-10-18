pkgname=dwm-patched
_pkgname=dwm
pkgver=6.4.r0.g50ad171
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft')
makedepends=('git')
install=dwm.install
provides=('dwm')
conflicts=('dwm' 'dwm-git')
_patches=('https://dwm.suckless.org/patches/statusallmons/dwm-statusallmons-6.2.diff'
          'dwm-focusmonmouse-6.2.diff'
          'https://dwm.suckless.org/patches/restartsig/dwm-restartsig-20180523-6.2.diff'
          'https://dwm.suckless.org/patches/restoreafterrestart/dwm-restoreafterrestart-20220709-d3f93c7.diff'
          'https://dwm.suckless.org/patches/layoutmenu/dwm-layoutmenu-6.2.diff'
          'https://dwm.suckless.org/patches/dragmfact/dwm-dragmfact-6.2.diff'
          'https://dwm.suckless.org/patches/cfacts/dwm-cfacts-20200913-61bb8b2.diff'
          'https://dwm.suckless.org/patches/cfacts/dwm-cfacts_bottomstack-6.2.diff'
          'https://dwm.suckless.org/patches/doublepressquit/dwm-doublepressquit-6.3.diff'
)
source=(dwm.desktop
        "$_pkgname::git+http://git.suckless.org/dwm"
        config.h
        "${_patches[@]}")
md5sums=('939f403a71b6e85261d09fc3412269ee'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP') # so you can customize config.h

pkgver(){
  cd $_pkgname
  git describe --long --tags | sed -E 's/([^-]*-g)/r\1/;s/-/./g'
}

prepare() {
  cd $_pkgname
  if [[ -f "$srcdir/config.h" ]]; then
    cp -fv "$srcdir/config.h" config.h
  fi

  for patch in "${_patches[@]}"; do
      echo "Applying patch $(basename $patch)..."
      patch -Np1 -i "$srcdir/$(basename $patch)" --verbose
  done
}

build() {
  cd $_pkgname
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $_pkgname
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -m644 -D LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -m644 -D README "$pkgdir/usr/share/doc/$pkgname/README"
  install -m644 -D ../dwm.desktop "$pkgdir/usr/share/xsessions/dwm.desktop"
}

# vim:set ts=2 sw=2 et:
