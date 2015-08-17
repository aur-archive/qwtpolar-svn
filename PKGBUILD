# Maintainer: Kévin Guilloy <kevin at guilloy dot ath dot cx>
pkgname=qwtpolar-svn
pkgver=110
pkgrel=2
pkgdesc="Qwt polar is an extension of the Qwt library to support polar plots."
arch=('i686' , 'x86_64')
url="http://qwtpolar.sourceforge.net/"
license=('Qwt License, Version 1.0')
depends=('qt' 'qwt')
conflicts=('qwtpolar')
makedepends=('qt subversion')

_svntrunk='https://qwtpolar.svn.sourceforge.net/svnroot/qwtpolar/trunk/qwtpolar'
_svnmod='qwtpolar'

build() {
  cd "$startdir/src"
  svn co $_svntrunk --config-dir ./ $_svnmod

  msg 'SVN checkout or server timeout'
  msg 'Building sofware...'

  cd qwtpolar/
  sed -i -e 's/$${QWT_POLAR_INSTALL_PREFIX}\/doc/\/usr\/share\/doc\/qwt\//' qwtpolarconfig.pri
  sed -i -e 's/$${QWT_POLAR_INSTALL_PREFIX}\/include/\/usr\/include\/qwt\//' qwtpolarconfig.pri
  sed -i -e 's/$${QWT_POLAR_INSTALL_PREFIX}\/lib/\/usr\/lib\//' qwtpolarconfig.pri
  sed -i -e 's/$${QWT_POLAR_INSTALL_PREFIX}\/features/\/usr\/share\/qwt\/features\//' qwtpolarconfig.pri
  sed -i -e 's/^.*QwtPolarDesigner//' qwtpolarconfig.pri
  sed -i -e 's/^.*QwtPolarExamples//' qwtpolarconfig.pri
  echo "INCLUDEPATH += /usr/include/qwt" >> qwtpolarbuild.pri

  qmake
  make

  cd ..
}

package() {
  cd "$startdir/src/qwtpolar"

  make INSTALL_ROOT="$pkgdir/" install
}