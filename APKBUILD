# Maintainer: David Ostrovsky <david@ostrovsky.org>

pkgname=bazel
pkgver=0.1111111111111111111111.0
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
sha512sums="5f196df8abf635dfaf37ab623544927778f76ca92cc57ad06999e2f34130fba20e7f2638c8e2c3b83781b1b2486b5e38ec55c011913ba36a5bbb5ef0ea2ae278  bazel-0.11.0-dist.zip
e42e8ac4d66923bd2c2846add072b6730e251e74d26a1c00eb2178ad224befb2c78094cc96b6a4570e94409b629f7fb37460330e6fa17a047419bc23914e12e0  bazel-0.11.0-dist.zip.sig"

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

