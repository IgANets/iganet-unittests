# IgANets-UnitTests

[![GitlabSync](https://github.com/IgANets/iganet-unittests/actions/workflows/gitlab-sync.yml/badge.svg)](https://github.com/IgANets/iganet-unittests/actions/workflows/gitlab-sync.yml)
[![build](https://github.com/IgANets/iganet-unittests/actions/workflows/cmake-multi-platform.yml/badge.svg)](https://github.com/IgANets/iganet-unittests/actions/workflows/cmake-multi-platform.yml)
[![Documentation](https://img.shields.io/badge/docs-mkdocs-blue.svg)](https://iganets.github.io/iganet/)
[![GitHub Releases](https://img.shields.io/github/release/iganets/iganet-unittests.svg)](https://github.com/iganets/iganet-unittests/releases)
[![GitHub Downloads](https://img.shields.io/github/downloads/iganets/iganet-unittests/total)](https://github.com/iganets/iganet-unittests/releases)
[![GitHub Issues](https://img.shields.io/github/issues/iganets/iganet-unittests.svg)](https://github.com/iganets/iganet-unittests/issues)

This directory contains unit tests for [IgANets](https://github.com/iganets/iganet), a novel approach to combine the concept of deep operator learning with the mathematical framework of isogeometric analysis.

## Usage instructions

This repository can be used in two modes:

1. As standalone unit tests by running CMake on _this_ repository without flags

2. As optional module in IgANets::core by running CMake on IgANets::core with the flag `-DIGANET_BUILD_UNITTESTS=ON`

In both cases, the tests can be run via
```shell
make test
```
