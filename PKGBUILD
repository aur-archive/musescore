# Maintainer: Stefan Husmann <stefan-husmann@t-online.de
# Contributor: Cristian Maureira <saint [at] archlinux.cl>
# Contributor: Dr.Egg <rwhite @ archlinux . us>

pkgname=musescore
pkgver=1.3
pkgrel=3
pkgdesc="A music score editor written in Qt"
arch=('i686' 'x86_64')
url="http://www.musescore.org/en/"
license=('GPL')
depends=('shared-mime-info' 'qtscriptgenerator' 'portaudio')
makedepends=('cmake' 'doxygen')
optdepends=('jack')
install=musescore.install
source=("http://downloads.sourceforge.net/mscore/mscore-${pkgver}.tar.bz2"
paths.patch system_qscriptgenerator.patch mime.xml qmake-qt4.patch desktop.patch)
md5sums=('e5fde2bef0d40ee7542e1f515a3919d1'
         '28f61c298f53214adacbc8d43f9c43e9'
         '51e590842a92cdea7efa01fd60fe715c'
         '969696178e56de36f9af37d7da61baaa'
         'a9e1d9c1a891810172245c6021682258'
         'c8f37720422ae1e1a0fa02b284bd00ed')

build() {
  cd $srcdir/mscore-${pkgver}
  export QT_PLUGINS_DIR=/usr/lib/qt4/plugins 
  [ -d build ] && make clean
  patch -p1 < $srcdir/system_qscriptgenerator.patch 
  patch -p1 < $srcdir/paths.patch
  patch -p1 < $srcdir/desktop.patch
  patch -p1 < $srcdir/qmake-qt4.patch 
  make PREFIX=/usr release 
}

package() {
  cd $srcdir/mscore-${pkgver}
  make PREFIX=/usr DESTDIR="$pkgdir" install
  cd $pkgdir/usr/share/mscore-$pkgver/man
  install -d $pkgdir/usr/share/doc/$pkgname
  cp * $pkgdir/usr/share/doc/$pkgname/
  cd ../..
  rm -r $pkgdir/usr/share/mscore-$pkgver/man
  install -Dm644 $srcdir/mime.xml \
    $pkgdir/usr/share/mime/packages/x-musescore.xml
}
