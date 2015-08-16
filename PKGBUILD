# Maintainer: Valere Monseur <valere dot monseur at ymail dot com>
# Contributor: Alexander Fehr <pizzapunk gmail com>

pkgname=ktsuss-svn
pkgver=9
pkgrel=2
pkgdesc="Graphical version of su written in C and GTK+"
arch=('i686' 'x86_64')
url="http://code.google.com/p/ktsuss"
license=('BSD')
depends=('gtk2')
provides=('ktsuss')
conflicts=('ktsuss')
makedepends=('subversion')

_svntrunk=http://ktsuss.googlecode.com/svn/trunk/
_svnmod=ktsuss

build() {
  cd "$srcdir"

  if [ -d "$_svnmod/.svn" ]; then
    (cd "$_svnmod" && svn up)
  else
    svn co "$_svntrunk" --config-dir ./ "$_svnmod"
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting make..."

  cd "$srcdir/$_svnmod"

  if [ ! -x ./configure ]; then
    ./autogen.sh
  fi

  ./configure --prefix=/usr --libexecdir=/usr/lib/ktsuss
  make
}

package() {
  cd "$srcdir/$_svnmod"

  make DESTDIR="$pkgdir" install
  install -D -m644 COPYING "$pkgdir/usr/share/licenses/ktsuss/COPYING"
}
