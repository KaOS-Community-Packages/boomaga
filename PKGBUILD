pkgname=boomaga
pkgver=1.3.0
pkgrel=1
pkgdesc="Boomaga (BOOklet MAnager) is a virtual printer for viewing a document before printing it out using the physical printer."
arch=('x86_64')
url='https://boomaga.github.io'
license=('LGPL' 'GPL')
depends=('cups' 'snappy' 'poppler' 'ghostscript')
makedepends=('cmake')
install=${pkgname}.install
source=("https://github.com/Boomaga/boomaga/archive/v${pkgver}.tar.gz")
sha256sums=('fd05be1100701cf6e7bbbf41b635ca2ca4d1eaf88bfdcf4a83f9a6ba8de24e35')

build() {
  cd ${srcdir}/${pkgname}-${pkgver}/
  [ -d build ] && rm -rf build
  mkdir -p build
  cd build

  cmake ../ \
    -DCMAKE_INSTALL_PREFIX:PATH=/usr \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_LIBDIR=/lib \
    -DKDE_INSTALL_USE_QT_SYS_PATHS=ON \
    -DQML_INSTALL_DIR=/usr/lib/qt5/qml \
    -DPLUGIN_INSTALL_DIR=/usr/lib/qt5/plugins \
    -DBUILD_TESTING=OFF
    
  make 
}

package() {
  cd ${srcdir}/${pkgname}-${pkgver}/build
  make DESTDIR=${pkgdir} all install
  install -Dm755 $srcdir/$pkgname-$pkgver/scripts/installPrinter.sh ${pkgdir}/usr/bin/installPrinter.sh
}
