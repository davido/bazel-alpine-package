# bazel-alpine-package

This is the Bazel 0.26.0 as a Alpine Linux package.

## Installing

The current installation method for these packages is to pull them in using `wget` or `curl` and install the local file with `apk`:

    apk --no-cache add ca-certificates wget
    wget -q -O /etc/apk/keys/david@ostrovsky.org-5a0369d6.rsa.pub https://raw.githubusercontent.com/davido/bazel-alpine-package/master/david@ostrovsky.org-5a0369d6.rsa.pub
    wget https://github.com/davido/bazel-alpine-package/releases/download/0.26.0/bazel-0.26.0-r0.apk
    apk add bazel-0.26.0-r0.apk

## Usage inside a Dockerfile

    ADD https://raw.githubusercontent.com/davido/bazel-alpine-package/master/david@ostrovsky.org-5a0369d6.rsa.pub \
        /etc/apk/keys/david@ostrovsky.org-5a0369d6.rsa.pub
    ADD https://github.com/davido/bazel-alpine-package/releases/download/0.26.0/bazel-0.26.0-r0.apk \
        /tmp/bazel-0.26.0-r0.apk
    RUN apk add /tmp/bazel-0.26.0-r0.apk
