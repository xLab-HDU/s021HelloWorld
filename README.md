# Hello World
This repository provides a CMake template for creating C++ projects.

[![Build Status](https://github.com/xLab-HDU/s021HelloWorld/actions/workflows/ci.yml/badge.svg)](https://github.com/xLab-HDU/s021HelloWorld/actions)

## How to Use

```sh
# configure the project
cmake -B build

# build the project
cmake --build build

# test the project
cd build
ctest --output-on-failure

# run the project
./bin/main.exe

# package the project
cpack -G ZIP
# or
cpack -G NSIS
```

## License

The source code is dual licensed under Public Domain and MIT -- choose whichever you prefer.
