```
$ docker build . -t bazel-centos-test
$ docker run --rm -it -v $(PWD):/src -w /src bazel-centos-test /bin/bash
# bazel build //...
```

