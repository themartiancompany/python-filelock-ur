# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Felix Yan <felixonmars@archlinux.org>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=filelock
_Pkg=py-filelock
pkgname="${_py}-${_pkg}"
pkgver=3.13.1
_commit=141f5d8c21be2830a9d93ad4ad822acf4b0f8a12
pkgrel=1
pkgdesc="A platform independent file lock"
_http="https://github.com"
_ns="benediktschmitt"
url="${_http}/${_ns}/${_Pkg}"
license=(
  'custom:Unlicense'
)
arch=(
  'any'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  'git'
  "${_py}-build"
  "${_py}-installer"
  "${_py}-hatchling"
  "${_py}-hatch-vcs"
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-pytest-timeout"
  "${_py}-pytest-mock"
)
source=(
  "git+${url}.git#commit=$_commit"
)
sha512sums=(
  'SKIP'
)

build() {
  cd \
    "${_Pkg}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation
}

check() {
  cd \
    "${_Pkg}"
  PYTHONPATH=src \
  pytest \
    tests
}

package() {
  cd \
    "${_Pkg}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -Dm644 \
    LICENSE \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
}

