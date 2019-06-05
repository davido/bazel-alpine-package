# Maintainer: David Ostrovsky <david@ostrovsky.org>

pkgname=bazel
pkgver=0.26.0
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
options="!distcc !strip !check"
source="https://github.com/bazelbuild/bazel/releases/download/${pkgver}/bazel-${pkgver}-dist.zip
        https://github.com/bazelbuild/bazel/releases/download/${pkgver}/bazel-${pkgver}-dist.zip.sig"

sha512sums="e3471bbd3daf44f9a34ed6f8125f666cc2297f1b9e32ac57259cdb45161fdbb9cf6a9595849746a69ba1164e4bb0c916d5cdf351d7b40eab9ce31972ec622ad7  bazel-0.26.0-dist.zip
ac4805ecd6a34a0782a2fefcdbbe8a2e9c6482b315b4f1dab49fc7bb1db13f03090d45629b5a7e4ed5af4f072d9460258a0b279e6f7edd129b4b20741326b7ab  bazel-0.26.0-dist.zip.sig"

build() {
  export JAVA_HOME=/usr/lib/jvm/default-jvm
  EXTRA_BAZEL_ARGS=--host_javabase=@local_jdk//:jdk ./compile.sh
  scripts/generate_bash_completion.sh --bazel=output/bazel --output=output/bazel-complete.bash --prepend=scripts/bazel-complete-template.bash
  output/bazel shutdown
  echo startup --server_javabase=$JAVA_HOME >> scripts/packages/bazel.bazelrc
}

package() {
  install -Dm755 ${srcdir}/scripts/packages/bazel.sh ${pkgdir}/usr/bin/bazel
  install -Dm755 ${srcdir}/scripts/packages/bazel.bazelrc ${pkgdir}/etc/bazel.bazelrc
  install -Dm755 ${srcdir}/output/bazel ${pkgdir}/usr/bin/bazel-real
  install -Dm644 ${srcdir}/output/bazel-complete.bash ${pkgdir}/usr/share/bash-completion/completions/bazel
  install -Dm644 ${srcdir}/scripts/zsh_completion/_bazel ${pkgdir}/usr/share/zsh/site-functions/_bazel
}
# vim:set ts=2 sw=2 et:

