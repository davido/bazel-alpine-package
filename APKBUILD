# Maintainer: David Ostrovsky <david@ostrovsky.org>

pkgname=bazel
pkgver=0.22.0
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

sha512sums="b93cd21f0f164c118b90efba761a9492eb9894e24f13ff468defd12b86c7e67f16e51060ac2fc4c2f8dbf51b1c833d41b255fdd8107988e5babf093cfc5b3254  bazel-0.22.0-dist.zip
65cedf12b5650ca0708b4fadeeefee1f3f680d6f09ba1e3ffe2e3d42855e558712feacb3f99566902d9f94b5ed0b763e3cc0b13dfd6ffb7046e73468d003faca  bazel-0.22.0-dist.zip.sig"

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

