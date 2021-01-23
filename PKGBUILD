# Maintainer katt <magunasu.b97@gmail.com>
# Contributor: Antonio Rojas <arojas@archlinux,org>

pkgname=dolphin-git
pkgver=20.12.1.r114.g8236e95c7
pkgrel=1
pkgdesc='KDE File Manager (Git)'
arch=(i686 x86_64)
url=https://kde.org/applications/en/system/org.kde.dolphin
license=(LGPL)
depends=(baloo-widgets knewstuff kio-extras kcmutils kparts kinit kactivities)
makedepends=(extra-cmake-modules-git kdoctools-git packagekit-qt5 git)
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
source=('git+https://invent.kde.org/system/dolphin.git'
	'0001-Revert-Disallow-executing-Dolphin-as-root-on-Linux.patch')
md5sums=('SKIP'
	'677fbd9b6ff947d67d8ae9ba25eb0e01')

pkgver() {
    git -C "${pkgname%-git}" describe --long | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}
prepare() {
  patch -p1 -d dolphin -i "$srcdir/0001-Revert-Disallow-executing-Dolphin-as-root-on-Linux.patch"
  cd $srcdir
}

build() {
    cmake -B build -S "${pkgname%-git}" \
        -DBUILD_TESTING=OFF
    cmake --build build
}

package() {
    DESTDIR="${pkgdir}" cmake --install build
}
