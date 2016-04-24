pkgname=boomaga
pkgver=0.7.1
pkgrel=1
pkgdesc="Boomaga (BOOklet MAnager) is a virtual printer for viewing a document before printing it out using the physical printer."
arch=('x86_64')
url='https://boomaga.github.io'
license=('LGPL' 'GPL')
depends=('cups' 'snappy' 'poppler' 'ghostscript')
makedepends=('cmake')
install=${pkgname}.install
source=("https://github.com/Boomaga/boomaga/archive/v${pkgver}.tar.gz")
sha512sums=('203bfe7edeb1d22e1923d35ef3160f6ec0744c5d9a50d3c22c89c72ce24d4083f7276a4f71e599d0b95f0d880a0634391b0699fb2eab0c3d04e0c0fcf91193cd')

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
