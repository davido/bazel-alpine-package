# bazel-alpine-package

This is the Bazel as a Alpine Linux package.

## Installing

The current installation method for these packages is to pull them in using `wget` or `curl` and install the local file with `apk`:

    apk --no-cache add ca-certificates wget
    wget -q -O /etc/apk/keys/david@ostrovsky.org-5a0369d6.rsa.pub https://raw.githubusercontent.com/davido/bazel-alpine-package/master/david@ostrovsky.org-5a0369d6.rsa.pub
    wget https://github.com/davido/bazel-alpine-package/releases/download/0.7.0/bazel-0.7.0-r1.apk
    apk add bazel-0.7.0-r1.apk
