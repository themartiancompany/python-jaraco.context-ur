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
pkgver=5.3.0
_commit="e0e9224b3dbe6520c986bf41820f882160dd55ab"
pkgrel=1
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
checkdepends=(
  "${_py}-portend"
  "${_py}-pytest"
)
makedepends=(
  "${_py}-setuptools-scm"
  "${_py}-build"
  "${_py}-installer"
  "${_py}-wheel"
)
# _tag="${_commit}"
# _tag_name="commit"
_tag="${pkgver}"
_tag_name="tag"
_tarname="${_pkg}-${_tag}"
_pypi="https://pypi.io/packages/source"
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    'git'
  )
  _src="${_tarname}::git+${url}.git#${_tag_name}=${_tag}"
  _sum="SKIP"
elif [[ "${_git}" == "false" ]]; then
  _src="${_tarname}.tar.gz::${_pypi}/${_pkg::1}/${_pkg}/${_pkg}-${pkgver}.tar.gz"
  _sum="c2f67165ce1f9be20f32f650f25d8edfc1646a8aeee48ae06fb35f90763576d2"
  # _src="${_tarname}.zip::${url}/archive/${_commit}.zip"
  # 5.3.0
  # _sum='6082cf806d60affa9625088dec55656e48afd0c5ab42aa139031c77a6cbe34822cd56b9cdf653c2d6b761b277caaf24b75c14ffa220bd5cda4b2e82dac73523d'
  # 6.0.1
  # _sum='353d3a3ad6fc2fdd66e4e701b13c725373ffd4d44ec91ecd31f5ae9194e7605175dff48ee8d84f81859283a984e2eacd56e7408a5604c55ce4075f16d3c7a67b'
fi
checkdepends=(
  "${_py}-pytest"
)
source=(
  "${_src}"
)
sha256sums=(
  "${_sum}"
)

build() {
  ls 
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
