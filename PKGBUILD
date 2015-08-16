# Maintainer : speps <speps at aur at archlinux dot org>
# Contributor: cga <cga@cga.cx>

pkgname=iannix
pkgver=0.8.43
pkgrel=1
pkgdesc="A score editor based on the UPIC sequencer by Iannis Xenakis."
arch=('i686' 'x86_64')
url="http://www.iannix.org/"
license=('GPL')
depends=('qt4' 'shared-mime-info')
makedepends=('automoc4')
install="$pkgname.install"
options=('!emptydirs')
#source=("${url}en/download/${pkgname}_linux__${pkgver//./_}.tar.gz"
source=("https://github.com/$pkgname/IanniX/tarball/IanniX-${pkgver//./-}"
        "x-$pkgname.desktop"
        "$pkgname.desktop"
        "$pkgname-mime.xml"
        "$pkgname.png")
md5sums=('d314e30943152b9ff2a086ea7ee4da52'
         'fced40a56f922f47581962e34864bb96'
         '80a4af3e4800d3c837d11d3d33e9f56e'
         'b2e86f51136ce7c923cb4fbae9e7e5a5'
         '6441847848fd185ad2ba2a1dfeb502c4')

prepare() {
  cd "$srcdir/$pkgname-IanniX-"*

  # let iannix fetch datas from /usr/share/iannix
  sed -i "s|\./|/usr/share/$pkgname/|g" $pkgname.cpp Tools/* Examples/*.nx{script,style}
  sed -i "s_\"\(Tools\|Examples\|Project\|Patches\|Documentation\)_\"/usr/share/$pkgname/\1_g" \
    $pkgname.cpp extoscpatternask.h extscriptmanager.cpp uirender.cpp uiview.h
}

build() {
  cd "$srcdir/$pkgname-IanniX-"*
  qmake-qt4 IanniX.pro
  make
}

package() {
  cd "$srcdir/$pkgname-IanniX-"*

  # bin
  install -Dm755 IanniX "$pkgdir/usr/bin/$pkgname"

  # data
  install -d "$pkgdir/usr/share/$pkgname"
  cp -a Examples Tools Patches Project Documentation \
    "$pkgdir/usr/share/$pkgname"
  rm -rf "$pkgdir/usr/share/$pkgname/Patches/Ableton"*

  # desktop
  install -Dm644 ../$pkgname.desktop \
    "$pkgdir/usr/share/applications/$pkgname.desktop"

  # icon
  install -Dm644 ../$pkgname.png \
    "$pkgdir/usr/share/pixmaps/$pkgname.png"

  # mime
  install -Dm644 ../x-$pkgname.desktop \
    "$pkgdir/usr/share/applications"
  install -Dm644 ../$pkgname-mime.xml \
    "$pkgdir/usr/share/mime/applications/$pkgname-mime.xml"

  # remove svn files and MACOSX .DS_Store
  rm -rf `find "$pkgdir" -type d -name ".svn"`
  find "$pkgdir" -name .DS_Store -delete
}
