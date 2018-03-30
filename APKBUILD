# Maintainer: David Ostrovsky <david@ostrovsky.org>

pkgname=bazel
pkgver=0.11.1
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
sha512sums="18648d277c8605c7321d3b2e3461c41983aaea0f5dee0832086cf87189888fddcfef0de422243490140e32b2ebf82f4883411753a343849f7aba25acfd0ce5f1  bazel-0.11.1-dist.zip
6570939b6c2ca1f24382d4f492b3704503265ada6111dd45247d2972cfa8e03143fe0d4bb6b0da4f7aea96a00e8b3c9a8ca97c5e37bacb7de42772f06eb4cf34  bazel-0.11.1-dist.zip.sig"

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

