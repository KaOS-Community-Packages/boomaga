pkgname=boomaga
pkgver=0.7.0
pkgrel=2
pkgdesc="Boomaga (BOOklet MAnager) is a virtual printer for viewing a document before printing it out using the physical printer."
arch=('x86_64')
url='https://boomaga.github.io'
license=('LGPL' 'GPL')
depends=('cups' 'snappy' 'poppler' 'ghostscript')
install=${pkgname}.install
source=("https://github.com/Boomaga/boomaga/archive/v0.7.0.tar.gz")
sha512sums=('8b85d95253db7724170f00aa98a8244f3fa3f0402cc7d26688cf84d805636f5a5f606846477271a4a4ce3d33105477da405e2d19b8e9ce66a4be922e77b3cecc')

build() {
  cd ${srcdir}/${pkgname}-${pkgver}/
  [ -d build ] && rm -rf build
  mkdir -p build
  cd build

  cmake ../ \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_LIBDIR=lib \
    -DKDE_INSTALL_USE_QT_SYS_PATHS=ON \
    -DQML_INSTALL_DIR=/usr/lib/qt5/qml \
    -DPLUGIN_INSTALL_DIR=/usr/lib/qt5/plugins \
    -DBUILD_TESTING=OFF
    
  make 
}

package() {
  cd ${srcdir}/${pkgname}-${pkgver}/build
  make DESTDIR=${pkgdir} install
  install -D -m755 $srcdir/$pkgname-$pkgver/scripts/installPrinter.sh ${pkgdir}/usr/bin/installPrinter.sh
}
