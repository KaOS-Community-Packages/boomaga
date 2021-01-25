pkgname=boomaga
pkgver=3.0.0
pkgrel=1
pkgdesc="Boomaga (BOOklet MAnager) is a virtual printer for viewing a document before printing it out using the physical printer."
arch=('x86_64')
url='https://boomaga.github.io'
license=('LGPL' 'GPL')
depends=('cups' 'snappy' 'poppler' 'ghostscript' 'qt5-tools')
makedepends=('cmake')
install=${pkgname}.install
source=("https://github.com/Boomaga/boomaga/archive/v${pkgver}.tar.gz")
md5sums=('2f25c8901acf748a53560f1f93565f90')

build() {
  cd ${srcdir}/${pkgname}-${pkgver}/
  [ -d build ] && rm -rf build
  mkdir -p build
  cd build

  cmake ../
  make -j$(nproc)
}

package() {
  cd ${srcdir}/${pkgname}-${pkgver}/build
  make DESTDIR=${pkgdir} all install
  install -Dm755 $srcdir/$pkgname-$pkgver/scripts/installPrinter.sh ${pkgdir}/usr/bin/installPrinter.sh
}
