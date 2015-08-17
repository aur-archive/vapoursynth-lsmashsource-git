# Maintainer:  Gustavo Alvarez <sl1pkn07@gmail.com>

_plug=lsmashsource
pkgname=vapoursynth-${_plug}-git
pkgver=r708.c7cc104
_pkgver="$(echo ${pkgver} | cut -d '.' -f1 | tr -d r)"
pkgrel=1
pkgdesc="Plugin for Vapoursynth: ${_plug} (GIT version)"
arch=('i686' 'x86_64')
url="https://github.com/VFR-maniac/L-SMASH-Works"
license=('GPL')
depends=('vapoursynth' 'l-smash-git')
provides=("vapoursynth-${_plug}")
conflicts=("vapoursynth-${_plug}" "vapoursynth-plugin-${_plug}")
makedepends=('git')
source=("${_plug}::git+https://github.com/VFR-maniac/L-SMASH-Works.git")
md5sums=('SKIP')
_gitname="${_plug}"

pkgver() {
  cd "${_gitname}"
  echo "r$(git rev-list HEAD 2> /dev/null | wc -l | sed 's/ //g').$(git describe --always)"
}

build() {
  cd "${_gitname}/VapourSynth"
  ./configure --prefix=/usr --extra-cflags="-fPIC"
  make
}

package(){
  cd "${_gitname}/VapourSynth"
  install -Dm755 "vslsmashsource.so.${_pkgver}" "${pkgdir}/usr/lib/vapoursynth/vslsmashsource.so.${_pkgver}"
  ln -s "/usr/lib/vapoursynth/vslsmashsource.so.${_pkgver}" "${pkgdir}/usr/lib/vapoursynth/vslsmashsource.so"
  install -Dm644 README "${pkgdir}/usr/share/doc/vapoursynth/plugins/${_plug}/README"
}
