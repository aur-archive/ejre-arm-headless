# Maintainer: Oleg Rakhmanov <orakhmanov [at] gmail [dot] com>
# Contributors: Charles Ghislain, Guillaume ALAUX, Daniel J Griffiths, Jason Chu, Geoffroy Carrier, Army, kfgz, Thomas Dziedzic, Dan Serban, jjacky, EasySly

pkgname=ejre-arm-headless
_major=7
_minor=60
_build=19
_date=07_may_2014


_pkgver=${_major}u${_minor}
pkgver=${_major}.${_minor}
pkgrel=2

pkgdesc="Oracle Embedded Java Runtime Environment for ARM - headless"
arch=('arm' 'armv6h' 'armv7h')
url=http://www.oracle.com/technetwork/java/javase/downloads/index.html
license=('custom')
depends=('shared-mime-info' 'xdg-utils')
optdepends=('alsa-lib: sound')
provides=("java-runtime=$_major" "java-runtime-headless=$_major")
conflicts=("${provides[@]}")
backup=('etc/profile.d/ejre.csh'
        'etc/profile.d/ejre.sh')
install=ejre-arm-headless.install

if [ "$CARCH" == "armv6h" -o "$CARCH" == "armv7h" ]; then
   #_source=ejre-${_major}u${_minor}-fcs-b${_build}-linux-arm-vfp-hflt-client_headless-${_date}.tar.gz
   _source=https://github.com/mrpickolous/ejre/archive/armv67.tar.gz
   _sourcemd5sum='12687090491d3acb3edc0cbb2676ab69'
   _subdir="ejre-armv67"
else
   #_source=ejre-${_major}u${_minor}-fcs-b${_build}-linux-arm-sflt-headless-${_date}.tar.gz
   _source=https://github.com/mrpickolous/ejre/archive/armv5.tar.gz
   _sourcemd5sum='6a43bd13c40ff9ba3a7ed2dff68983f4'
   _subdir="ejre-armv5"
fi

source=("${_source}"
        'ejre.csh'
        'ejre.sh')

md5sums=(${_sourcemd5sum}
         '6fdb3e968f76bdc56cbe7bdb720e3dcc'
         'fccc55f6ac29f16dd08d5ac167b80ee4')

package() {
  msg2 "Creating required dirs"
  cd "${_subdir}/ejre1.$_major.0_$_minor"
  mkdir -p "$pkgdir"/{opt/java/ejre,usr/share/licenses/ejre,etc/profile.d}

  msg2 "Moving stuff in place"
  mv COPYRIGHT *.txt "$pkgdir"/usr/share/licenses/ejre/
  mv * "$pkgdir"/opt/java/ejre/

  msg2 "Installing the scripts, confs of our own"
  cd "$srcdir"
  install -m755 ejre.{,c}sh "$pkgdir"/etc/profile.d/
}
