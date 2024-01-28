# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Truocolo <truocolo@aol.com>

_proj="jaraco"
_pkg="${_proj}.context"
_py="python"
pkgname="${_py}-${_pkg}"
pkgver=4.3.0
_commit=0e0ae08919b984e3c7cffdb2106e437d0d0891c8
pkgrel=3
pkgdesc="Context managers by jaraco"
url="https://github.com/${_proj}/${_pkg}"
license=(
  'MIT'
)
arch=(
  'any'
)
depends=(
  "${_py}"
)
makedepends=(
  'git'
  "${_py}-setuptools-scm"
  "${_py}-build"
  "${_py}-installer"
  "${_py}-wheel"
)
checkdepends=(
  "${_py}-pytest"
)
source=(
  "git+${url}.git#commit=${_commit}"
)
sha512sums=(
  'SKIP'
)

build() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m build \
    -wn
}

check() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      pytest
}

package() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -Dm644 \
    LICENSE \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim:set sw=2 sts=-1 et:
