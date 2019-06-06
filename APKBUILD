# Maintainer: David Ostrovsky <david@ostrovsky.org>

pkgname=bazel
pkgver=0.26.1
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

sha512sums="f43f156947c2e9effb1f3ab79235d47d00254103b5a5aac62001008403216b2330c9062ce85d42be4fa582ad52d14ba52a47875df40c58a7e18c391684407574  bazel-0.26.1-dist.zip
3e12a12a0a8a72e226451f1454f7a0e19b56d94cb03440e196657059b9687792ad030e3be1af34ee35883d5ee54027f5924af1b8fe9e71ce90e76abed7a2213f  bazel-0.26.1-dist.zip.sig"

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

