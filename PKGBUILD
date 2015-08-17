# Maintainer: Jonathan Liu <net147@gmail.com>
pkgname=osmesa
pkgver=8.0.2
pkgrel=1
pkgdesc="Mesa 3D off-screen rendering library"
arch=('i686' 'x86_64')
url="http://mesa3d.sourceforge.net"
license=('custom')
depends=("mesa")
makedepends=('imake' 'libxml2' 'python2')
options=('!makeflags')
source=("ftp://ftp.freedesktop.org/pub/mesa/${pkgver}/MesaLib-${pkgver}.tar.bz2"
        "LICENSE")
md5sums=('a368104e5700707048dc3e8691a9a7a1'
         '5c65a0fe315dd347e09b1f2826a1df5a')

build() {
  cd "${srcdir}/Mesa-${pkgver}"
  find . -name '*.py' -exec sed -i -r "s|#\s*!\s*(/usr)?/bin/(env\s*)?python\s*$|#!/usr/bin/env python2|" {} +
  sed -i -e "s|PYTHON2 = python|PYTHON2 = python2|" configs/{default,autoconf.in}
  sed -i -e "s|python|python2|" src/gallium/{auxiliary,drivers/llvmpipe}/{Makefile,SConscript}
  sed -i -e "s|python|python2|" src/mesa/drivers/dri/common/xmlpool/Makefile
  ./configure --prefix=/usr --disable-egl --disable-gallium-llvm --disable-glu --disable-dri --disable-glx --enable-osmesa --with-dri-drivers="" --with-gallium-drivers=""
  make
}

package() {
  cd "${srcdir}/Mesa-${pkgver}"
  make -C src/mesa DESTDIR="${pkgdir}" install-osmesa
  install -D -m755 "${srcdir}/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

# vim:set ts=2 sw=2 et:
