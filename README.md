# OpenVDB Sample Project

It's a little tricky to figure out how to use OpenVDB, so I put this together
to show how to build their code examples. I've only tested on Ubuntu 16.04 and
Ubuntu 18.04.

The C++ code comes directly from the [OpenVDB code examples][1].
FindOpenVDB.cmake comes from the OpenVDB repository, though I made a couple
modifications so it could find system libraries. Those modifications, and all
other code written by me in this repository is licensed under the [Creative
Commons Zero (CC0 1.0) license][2].

## Ubuntu Dependencies

    sudo apt install cmake build-essential \
        libopenvdb-dev libopenexr-dev libtbb-dev \
        libboost-dev extra-cmake-modules

## How to Build

    # developer build
    cmake -H. -Bbuild && cmake --build build

    # release build
    cmake -H. -Brelease -DCMAKE_BUILD_TYPE=Release && cmake --build release

[1]: http://www.openvdb.org/documentation/doxygen/codeExamples.html
[2]: https://creativecommons.org/publicdomain/zero/1.0/
