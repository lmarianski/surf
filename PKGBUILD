# Maintainer: cdude
# Contributor: sekret

_pkgname=surf
pkgname=$_pkgname-git
pkgver=2.1.r5.g11dca18
pkgrel=1
pkgdesc="a simple web broser based on WebKit2/GTK+"
arch=('i686' 'x86_64')
url="http://surf.suckless.org/"
license=('custom:MIT/X')
depends=('webkit2gtk' 'gcr' 'xorg-xprop')
makedepends=('git')
optdepends=('dmenu: url bar and search'
            'tabbed: tab browsing'
            'ca-certificates: SSL verification'
            'st: default terminal for the download handler'
            'curl: default download handler'
            'mpv: default video player')
provides=("$_pkgname")
conflicts=("$_pkgname")
source=("git+https://git.suckless.org/${_pkgname}"
        https://surf.suckless.org/patches/web-search/surf-websearch-20190510-d068a38.diff
        surf-websearch-fix.patch
        surf-popup-2.0.diff
)
md5sums=('SKIP'
         '7cf6fdef8ae73a07d6cd22491c7b365b'
         '2fbe920776a34484a3f210110a4c5df9'
         '572a30ff722d6f53e8d27f0763eccb48')

pkgver() {
  cd "$srcdir/$_pkgname"
  git describe --long --tags | sed -r 's/([^-]*-g)/r\1/;s/-/./g'
}

prepare() {
  cd "$srcdir/$_pkgname"

	# patch --input "$srcdir/surf-selection-clipboard.patch"   || echo
  patch --input "$srcdir/surf-websearch-20190510-d068a38.diff"   || echo
	patch --input "$srcdir/surf-websearch-fix.patch"   || echo
	patch --input "$srcdir/surf-popup-2.0.diff"   || echo

  if [ -e "$BUILDDIR/config.h" ]
	then
		cp "$BUILDDIR/config.h" .
	elif [ ! -e "$BUILDDIR/config.def.h" ]
	then
		msg='This package can be configured in config.h. Copy the config.def.h '
		msg+='that was just placed into the package directory to config.h and '
		msg+='modify it to change the configuration. Or just leave it alone to '
		msg+='continue to use default values.'
		echo "$msg"
	fi
	cp config.def.h "$BUILDDIR"
}

build() {
  cd "$srcdir/$_pkgname"
  make PREFIX=/usr DESTDIR="$pkgdir"
}

package() {
  cd "$srcdir/$_pkgname"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
