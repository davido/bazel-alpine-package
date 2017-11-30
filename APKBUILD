# Maintainer: davido <david@ostrovsky.org>

pkgname=bazel
pkgver=0.8.0
pkgrel=0
pkgdesc='Correct, reproducible, and fast builds for everyone'
arch="all"
license="ASL-2.0"
url='https://bazel.io/'
depends="openjdk8 libarchive zip unzip"
makedepends="git protobuf python"
options="!distcc !strip"
source="https://github.com/bazelbuild/bazel/releases/download/${pkgver}/bazel-${pkgver}-dist.zip
        https://github.com/bazelbuild/bazel/releases/download/${pkgver}/bazel-${pkgver}-dist.zip.sig"
sha512sums="742eecf6f141632ecad25dcee978942004c1b37966c42cff2c1a5e97a01c0870d61959eb6b1d038d5a26ff2338871a2cdb65fa4fc02e37beca76b89981c837e1  bazel-0.8.0-dist.zip
3f53609bdf6b011fbd411ea2cec68c064efda37fe87509c44bc29200daf6f7650f45545f372cbce4dd69570a13f462087fe9bd5c7b4c95ba0776d2580cd63803  bazel-0.8.0-dist.zip.sig"

build() {
  ./compile.sh
  # Patch bazel: https://github.com/bazelbuild/bazel/issues/4055
  # https://bugs.alpinelinux.org/issues/8121
  sed -i.bak 's/expr --/expr/' scripts/generate_bash_completion.sh
  ./output/bazel build -s --verbose_failures scripts:bazel-complete.bash
  cd output
  ./bazel shutdown
}

package() {
  install -Dm755 ${srcdir}/scripts/packages/bazel.sh ${pkgdir}/usr/bin/bazel
  install -Dm755 ${srcdir}/output/bazel ${pkgdir}/usr/bin/bazel-real
  install -Dm644 ${srcdir}/bazel-bin/scripts/bazel-complete.bash ${pkgdir}/usr/share/bash-completion/completions/bazel
  install -Dm644 ${srcdir}/scripts/zsh_completion/_bazel ${pkgdir}/usr/share/zsh/site-functions/_bazel
}
# vim:set ts=2 sw=2 et:
