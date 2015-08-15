# Contributor: dale <dale@archlinux.org>
# Maintainer: MCMic <come.bernigaud@laposte.net>

pkgname=gtetrinet
pkgver=0.7.11
pkgrel=4
pkgdesc="A clone of the game Tetrinet for the gnome environment."
arch=(i686 x86_64)
license=('GPL')
depends=('libgnomeui>=2.18.1-2')
makedepends=('libxml-perl' 'pkgconfig')
install=gtetrinet.install
url="http://gtetrinet.sourceforge.net/"
source=(http://ftp.gnome.org/pub/GNOME/sources/gtetrinet/0.7/${pkgname}-${pkgver}.tar.bz2)
md5sums=('7d113e49506e44b836ce6f259fd3ad88')

build() {
  cd ${srcdir}/${pkgname}-${pkgver}
  ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var
  sed -i -e 's/games$/bin/g' src/Makefile || return 1
  make || return 1
}

package () {
  cd ${srcdir}/${pkgname}-${pkgver}
  make GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL=1 DESTDIR=${pkgdir} install

  mkdir -p ${pkgdir}/usr/share/gconf/schemas
  gconf-merge-schema ${pkgdir}/usr/share/gconf/schemas/${pkgname}.schemas ${pkgdir}/etc/gconf/schemas/*.schemas
  rm -f ${pkgdir}/etc/gconf/schemas/*.schemas
}
