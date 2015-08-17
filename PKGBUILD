# Maintainer: Gustavo Alvarez <sl1pkn07@gmail.com>
# Contributor: totoloco <totoloco@gmx.com>

pkgname="sigram-git"
pkgver=r220.619e9e1
pkgrel=1
pkgdesc="A different telegram client from Sialan.labs (GIT version)"
arch=('i686' 'x86_64')
url="http://labs.sialan.org/projects/sigram"
license=('GPL')
depends=('qt5-graphicaleffects' 'qt5-quickcontrols')
makedepends=('git')
provides=('sigram')
conflicts=('sigram' 'sigram-bin')
source=('git+https://github.com/sialan-labs/sigram.git'
        'sigram.sh')
sha1sums=('SKIP'
          '6dce54be63fd4df22ba2ba2e7d05cc6772daafc1')
_gitname=sigram

pkgver() {
  cd "${_gitname}"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd "${_gitname}"
  sed 's|/opt/$${TARGET}/bin|/usr/share/sigram|g' -i Sigram/deployment.pri
}

build() {
  cd "${_gitname}"
  qmake SialanTelegram.pro
  make
}

package() {
  cd "${_gitname}"
  make INSTALL_ROOT="${pkgdir}" install
  install -d "${pkgdir}/usr/share/${_gitname}"
  cp -R build/* "${pkgdir}/usr/share/${_gitname}"
  install -Dm755 "${srcdir}/sigram.sh" "${pkgdir}/usr/bin/Sigram"
  install -Dm644 build/icons/icon.png "${pkgdir}/usr/share/pixmaps/sigram.png"
}

