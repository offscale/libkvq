libkvq
======
Library implementing key/value abstraction over multiple stores.

## Dependencies

  - C compiler
  - [CMake](https://cmake.org)
  - [conan](https://conan.io)

## Developer workflow

    mkdir cmake-build-debug && cd $_
    conan install ..
    cmake -DCMAKE_BUILD_TYPE=Debug -DTEST_ENABLED=1 ..
    ctest

## Run tests

Starting from directory created above, after `make` step, run:

    ./bin/test_*

---

## Roadmap

 - [Redis](https://redis.io)
 - [Zookeeper](https://zookeeper.apache.org)
 - [memcached](https://memcached.org)
 - [etcd](https://coreos.com/etcd)
   - [v2](https://github.com/etcd-io/etcd/releases/tag/v2.3.7)
   - [v3](https://github.com/etcd-io/etcd/releases)
 - [Consul](https://consul.io)
