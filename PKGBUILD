# Maintainer: Federico Cinelli <cinelli.federico@gmail.com>
# Contributor: Samuel Tardieu <sam@rfc1149.net>

pkgname=pygments-hg
pkgver=1615
pkgrel=1
pkgdesc="Python syntax highlighter"
arch=('any')
url="http://pygments.org/"
license=('BSD')
depends=('python2-distribute')
makedepends=('mercurial')
conflicts=("python-pygments")
provides=("python-pygments")

_hgroot="http://bitbucket.org/birkenfeld/"
_hgrepo="pygments-main"

build() {
  cd "$srcdir"
  msg "Connecting to Mercurial server...."
  
  if [ -d "$_hgrepo" ] ; then
    cd "$_hgrepo"
    hg pull -u 
    msg "The local files are updated."
  else
    hg clone "$_hgroot/$_hgrepo"
  fi

  msg "Mercurial checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_hgrepo-build"
  cp -r "$srcdir/$_hgrepo" "$srcdir/$_hgrepo-build"
  cd "$srcdir/$_hgrepo-build"
 
  python2 setup.py install --root="$pkgdir"
  install -Dm644 external/pygments.bashcomp "$pkgdir/etc/bash_completion.d/pygments"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
