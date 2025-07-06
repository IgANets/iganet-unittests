# IgANets-UnitTests

This directory contains unit tests for the [IgANets](https://github.com/iganets/iganet), a novel approach to combine the concept of deep operator learning with the mathematical framework of isogeometric analysis.

## Usage instructions

This repository can be used in two modes:

1. As optional module in IgANets::core by running CMake on IgANets::core with the flag `-DIGANET_BUILD_UNITTESTS=ON`

2. As standalone unit tests by running CMake on _this_ repository without flags

In both cases, the tests can be run via
```shell
make test
```

