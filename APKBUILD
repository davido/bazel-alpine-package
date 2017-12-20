# Maintainer: David Ostrovsky <david@ostrovsky.org>

pkgname=bazel
pkgver=0.9.0
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
sha512sums="94393b968201f4f3977e2fdd58f47a6dc9dc07ad24d95a0d955049ccf38e1c0d48fe0f4ff2f3f30844e1137ee77a8e1f5567db05a8681149582a2dc0b221b8f7  bazel-0.9.0-dist.zip
dabd9bc77719030cf7e29d0d6ed07090535fe052cf85956c630876d6b8ab6c1676c3c7bf91489b2086723a05e42a23404c448042cc6773df91edccb099330adc  bazel-0.9.0-dist.zip.sig"

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

