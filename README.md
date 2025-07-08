# IgANets-UnitTests

[![GitlabSync](https://github.com/IgANets/iganet-unittests/actions/workflows/gitlab-sync.yml/badge.svg)](https://github.com/IgANets/iganet-unittests/actions/workflows/gitlab-sync.yml)
[![build](https://github.com/IgANets/iganet-unittests/actions/workflows/cmake-multi-platform.yml/badge.svg)](https://github.com/IgANets/iganet-unittests/actions/workflows/cmake-multi-platform.yml)

This directory contains unit tests for [IgANets](https://github.com/iganets/iganet), a novel approach to combine the concept of deep operator learning with the mathematical framework of isogeometric analysis.

## Usage instructions

This repository can be used in two modes:

1. As standalone unit tests by running CMake on _this_ repository without flags

2. As optional module in IgANets::core by running CMake on IgANets::core with the flag `-DIGANET_BUILD_UNITTESTS=ON`

In both cases, the tests can be run via
```shell
make test
```
