# Maintainer: David Ostrovsky <david@ostrovsky.org>

pkgname=bazel
pkgver=0.15.2
pkgrel=0
pkgdesc='Correct, reproducible, and fast builds for everyone'
arch="all"
license="ASL-2.0"
url='https://bazel.io/'
depends="bash openjdk8 libarchive zip unzip"
# coreutils can be removed as a make dependency once expr in busybox is compatible with the BSD version, see following bug reports:
# Patch bazel: https://github.com/bazelbuild/bazel/issues/4055
# https://bugs.alpinelinux.org/issues/8121
makedepends="coreutils git linux-headers protobuf python"
options="!distcc !strip"
source="https://github.com/bazelbuild/bazel/releases/download/${pkgver}/bazel-${pkgver}-dist.zip
        https://github.com/bazelbuild/bazel/releases/download/${pkgver}/bazel-${pkgver}-dist.zip.sig"

sha512sums="c1257fc7eeadc8e76fbd52be393d07161e6eadf7111e09ee9a7f9bf6d3b7e848e9b193a3b66a13e99c09a42e577404cb3a5f1fc3819f35436a36149dbb1ea365  bazel-0.15.2-dist.zip
d81fd679b9efbd334a32ed4d32561deed7aace24f12462a5860d3fc7b4fc2dfa3614a23f4772e54d06031b364790e91df936d34b1f881ed4067234a8d84cc0b9  bazel-0.15.2-dist.zip.sig"

build() {
  ./compile.sh
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

