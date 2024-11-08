# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Baptiste Jonglez <archlinux at bitsofnetworks dot org>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Bart Verhagen <barrie.verhagen at gmail dot com>

pkgname=catch2
pkgver=3.6.0
pkgrel=1
_pkgdesc=(
  "Modern, C++-native, header-only,"
  "test framework for unit-tests, TDD and BDD"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'x86_64'
  'arm'
  'armv7l'
  'aarch64'
  'i686'
  'pentium4'
  'mips'
)
_http="https://github.com"
_ns="catchorg"
url="${_http}/${_ns}/${pkgname}"
license=(BSL-1.0)
# only needed when building shared library
# depends=(
#   'gcc-libs'
#   'glibc'
# ) 
makedepends=(
  git
  cmake
  python  # python seems to be necessary for building tests (FS#60273)
)
conflicts=('catch2-v2')
source=(
  ${pkgname}::"git+${url}#tag=v${pkgver}?signed")
sha512sums=(
  '2abfe4eef3928baf996773c549b599834e970ace19e8bea02b18e130c4186860e334bfba7badba04f60cbbd43a1c545cd4c032f729888fdbb2d2bbe11c02ae46'
)
validpgpkeys=(
  E29C46F3B8A7502860793B7DECC9C20E314B2360 # Martin Hořeňovský
  81E70B717FFB27AFDB45F52090BBFF120F9C087B # Jozef Grajciar
)

build() {
  # our recent default flags break test 1 (ApprovalTests)
  unset \
    CXXFLAGS
  cmake \
    -B \
      "${pkgname}"/build \
    -S \
      "${pkgname}" \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=lib \
    -DCATCH_BUILD_EXAMPLES=OFF \
    -DCATCH_ENABLE_COVERAGE=OFF \
    -DCATCH_ENABLE_WERROR=OFF \
    -DBUILD_TESTING=OFF \
    -DBUILD_SHARED_LIBS=OFF
    # -DBUILD_TESTING=ON \
    # -DCATCH_BUILD_TESTING=ON \
    # -DCATCH_DEVELOPMENT_BUILD=ON -Wno-dev \
    # -DCATCH_BUILD_EXTRA_TESTS=ON 
  cmake \
    --build \
    "${pkgname}/build"
}

#check() {
#  # test are only built whith build option
#  #  -DCATCH_DEVELOPMENT_BUILD=ON
#  ctest --test-dir "${pkgname}"/build
#}

package() {
  DESTDIR="${pkgdir}" \
  cmake \
    --install \
    "${pkgname}/build"
}

# vim: ts=2 sw=2 et:
