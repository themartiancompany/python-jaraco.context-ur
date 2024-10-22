# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Truocolo <truocolo@aol.com>

_git="true"
_os="$( \
  uname \
    -o)"
if [[ "${_os}" == "Android" ]]; then
  _git="false"
fi
_proj="jaraco"
_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_proj="jaraco"
_pkg="${_proj}.context"
_py="python"
pkgname="${_py}-${_pkg}"
pkgver=4.3.0
_commit="0e0ae08919b984e3c7cffdb2106e437d0d0891c8"
pkgrel=3
pkgdesc="Context managers by jaraco"
_http="https://github.com"
url="${_http}/${_proj}/${_pkg}"
license=(
  'MIT'
)
arch=(
  'any'
)
depends=(
  "${_py}>=${_pymajver}"
)
makedepends=(
  "${_py}-setuptools-scm"
  "${_py}-build"
  "${_py}-installer"
  "${_py}-wheel"
)
_tag="${_commit}"
_tag_name="commit"
_tarname="${_pkg}-${_tag}"
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    'git'
  )
  _src="${_tarname}::git+${url}.git#${_tag_name}=${_tag}"
  _sum="SKIP"
elif [[ "${_git}" == "false" ]]; then
  _src="${_tarname}.zip::${url}/archive/${_commit}.zip"
  _sum="bb6ce7a4e2c9ef94d7ca1e4ad45a550b97454f7b9fbf2b4c8d2235cfe3615b52"
fi
checkdepends=(
  "${_py}-pytest"
)
source=(
  "${_src}"
)
sha512sums=(
  "${_sum}"
)

build() {
  cd \
    "${_tarname}"
  "${_py}" \
    -m build \
    -wn
}

check() {
  cd \
    "${_tarname}"
  "${_py}" \
    -m \
      pytest
}

package() {
  cd \
    "${_tarname}"
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
