# Maintainer: davido <david@ostrovsky.org>

pkgname=bazel
pkgver=0.7.0
pkgrel=1
pkgdesc='Correct, reproducible, and fast builds for everyone'
arch="all"
license="ASL-2.0"
url='https://bazel.io/'
depends="openjdk8 libarchive zip unzip"
makedepends="git protobuf python"
options="!distcc !strip"
source="https://github.com/bazelbuild/bazel/releases/download/${pkgver}/bazel-${pkgver}-dist.zip
        https://github.com/bazelbuild/bazel/releases/download/${pkgver}/bazel-${pkgver}-dist.zip.sig"
sha512sums="039ab6a04fd4422bd14503187e6cc0d07301723b3ecae906606fa12ccea72190d82237899c103c1adfdf05dc8672887790780ddfb4cce87cd590adbde3d3f6d4  bazel-0.7.0-dist.zip
4f89f8e14697bca06745db4bdc956ea8042ec60545827583092d0749822d73cabdc3c2744d38e9b37dd91bc318a9f3cb74e62c4509c2566076c8102b4eeaaa9b  bazel-0.7.0-dist.zip.sig"

build() {
  ./compile.sh
  # Patch bazel: https://github.com/bazelbuild/bazel/issues/4055
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
