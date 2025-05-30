[![Build Status](https://github.com/libbitcoin/libbitcoin-build/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/libbitcoin/libbitcoin-build)

# Libbitcoin Build

*Libbitcoin Build System*

Libbitcoin Build uses templates and XML data to generate build artifacts for the following libbitcoin libraries.

See [MAINTAINED.md](MAINTAINED.md) for a list of artifacts maintained by this project.

* [![libbitcoin](https://github.com/libbitcoin/libbitcoin-system/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/libbitcoin/libbitcoin-system) [![Coverage Status](https://coveralls.io/repos/libbitcoin/libbitcoin-system/badge.svg)](https://coveralls.io/r/libbitcoin/libbitcoin-system) libbitcoin-system
* [![libbitcoin-blockchain](https://github.com/libbitcoin/libbitcoin-blockchain/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/libbitcoin/libbitcoin-blockchain) [![Coverage Status](https://coveralls.io/repos/libbitcoin/libbitcoin-blockchain/badge.svg)](https://coveralls.io/r/libbitcoin/libbitcoin-blockchain) libbitcoin-blockchain
* [![libbitcoin-client](https://github.com/libbitcoin/libbitcoin-client/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/libbitcoin/libbitcoin-client) [![Coverage Status](https://coveralls.io/repos/libbitcoin/libbitcoin-client/badge.svg)](https://coveralls.io/r/libbitcoin/libbitcoin-client) libbitcoin-client
* [![libbitcoin-consensus](https://github.com/libbitcoin/libbitcoin-consensus/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/libbitcoin/libbitcoin-consensus) [![Coverage Status](https://coveralls.io/repos/libbitcoin/libbitcoin-consensus/badge.svg)](https://coveralls.io/r/libbitcoin/libbitcoin-consensus) libbitcoin-consensus
* [![libbitcoin-database](https://github.com/libbitcoin/libbitcoin-database/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/libbitcoin/libbitcoin-database) [![Coverage Status](https://coveralls.io/repos/libbitcoin/libbitcoin-database/badge.svg)](https://coveralls.io/r/libbitcoin/libbitcoin-database) libbitcoin-database
* [![libbitcoin-explorer](https://github.com/libbitcoin/libbitcoin-explorer/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/libbitcoin/libbitcoin-explorer) [![Coverage Status](https://coveralls.io/repos/libbitcoin/libbitcoin-explorer/badge.svg)](https://coveralls.io/r/libbitcoin/libbitcoin-explorer) libbitcoin-explorer
* [![libbitcoin-network](https://github.com/libbitcoin/libbitcoin-network/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/libbitcoin/libbitcoin-network) [![Coverage Status](https://coveralls.io/repos/libbitcoin/libbitcoin-network/badge.svg)](https://coveralls.io/r/libbitcoin/libbitcoin-network) libbitcoin-network
* [![libbitcoin-node](https://github.com/libbitcoin/libbitcoin-node/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/libbitcoin/libbitcoin-node) [![Coverage Status](https://coveralls.io/repos/libbitcoin/libbitcoin-node/badge.svg)](https://coveralls.io/r/libbitcoin/libbitcoin-node) libbitcoin-node
* [![libbitcoin-protocol](https://github.com/libbitcoin/libbitcoin-protocol/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/libbitcoin/libbitcoin-protocol) [![Coverage Status](https://coveralls.io/repos/libbitcoin/libbitcoin-protocol/badge.svg)](https://coveralls.io/r/libbitcoin/libbitcoin-protocol) libbitcoin-protocol
* [![libbitcoin-server](https://github.com/libbitcoin/libbitcoin-server/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/libbitcoin/libbitcoin-server) [![Coverage Status](https://coveralls.io/repos/libbitcoin/libbitcoin-server/badge.svg)](https://coveralls.io/r/libbitcoin/libbitcoin-server) libbitcoin-server

Notes on Badges
* `libitcoin-client` coverage does not reflect the effect of `libitcoin-explorer` network tests.
* `libitcoin-explorer` coverage does not reflect the effect of network tests.
* `libitcoin-network` coverage does not reflect the effect of network tests.
* Current converage is inflated by the fact that only files with some level of coverage are counted.

The artifacts generated for each library are as follows. Package names coincide with libbitcoin repository names.

```
.appveyor.yml
.travis.yml
autogen.sh
build.cmd
configure.ac
install.sh
[library].pc.in
[library]_test_runner.sh
Makefile.am
include/bitcoin/[library].hpp
include/bitcoin/[library]/version.hpp
builds/cmake/CMakeLists.txt
builds/cmake/modules/[module].cmake
builds/msvc/nuget.config
builds/msvc/build/build_base.bat
builds/msvc/[edition]/[library]/[library].props
builds/msvc/[edition]/[library]/[library].vcxproj
builds/msvc/[edition]/[library]/[library].vcxproj.filters
builds/msvc/[edition]/[library]/[library].xml
builds/msvc/[edition]/[library]/packages.config
builds/msvc/[edition]/[library].import.props
builds/msvc/[edition]/[library].import.xml
builds/msvc/[edition]/[library].sln
```

These artifacts are merged into their respective repositories by libbitcoin maintainers. There is no need to build libbitcoin-build if you are not a maintainer in the process of applying a build configuration change.

The build system has a dependency on [iMatix GSL](https://github.com/imatix/gsl), recently moved to the [ZeroMQ repository](https://github.com/zeromq/gsl). There are Linux/OSX and Visual Studio builds of GSL. A recent version is recommended. There is also a Windows single file executable available for [download](https://github.com/imatix/gsl/releases/download/NuGet-4.1.0.1/gsl.exe).

![Dependencies](https://raw.githubusercontent.com/libbitcoin/libbitcoin-build/master/img/dependencies.png)

### Quick Start

This is similar to the [.travis.yml](https://github.com/libbitcoin/libbitcoin-build/blob/master/.travis.yml) and is useful for local generation. In addition to `generate.sh` there is a `generate.cmd` for the native Windows environment.

#### Linux
```
# Create a top-level work_directory.
work_directory=$HOME/work
mkdir -p $work_directory
cd $work_directory

# Clone, build and install the gsl dependency.
# gsl requires pcre package (e.g. libpcre3-dev)
# On Ubuntu: sudo apt-get install libpcre3-dev
git clone https://github.com/imatix/gsl.git
cd gsl/src
make && sudo make install
cd ../../

# Clone all libbitcoin repositories.
git clone https://github.com/libbitcoin/libbitcoin-system.git
git clone https://github.com/libbitcoin/libbitcoin-blockchain.git
git clone https://github.com/libbitcoin/libbitcoin-build.git
git clone https://github.com/libbitcoin/libbitcoin-client.git
git clone https://github.com/libbitcoin/libbitcoin-consensus.git
git clone https://github.com/libbitcoin/libbitcoin-database.git
git clone https://github.com/libbitcoin/libbitcoin-explorer.git
git clone https://github.com/libbitcoin/libbitcoin-network.git
git clone https://github.com/libbitcoin/libbitcoin-node.git
git clone https://github.com/libbitcoin/libbitcoin-protocol.git
git clone https://github.com/libbitcoin/libbitcoin-server.git

# Run the libbitcoin-build generation script.
# Newly generated build files are copied to the cloned repos.
cd libbitcoin-build
./generate.sh
```
#### Windows
```
REM Create a top-level work_directory.
set work_directory=%USERPROFILE%\work
if not exist %work_directory% mkdir %work_directory%
cd %work_directory%

REM Clone all libbitcoin repositories.
git clone https://github.com/libbitcoin/libbitcoin-system.git
git clone https://github.com/libbitcoin/libbitcoin-blockchain.git
git clone https://github.com/libbitcoin/libbitcoin-build.git
git clone https://github.com/libbitcoin/libbitcoin-client.git
git clone https://github.com/libbitcoin/libbitcoin-consensus.git
git clone https://github.com/libbitcoin/libbitcoin-database.git
git clone https://github.com/libbitcoin/libbitcoin-explorer.git
git clone https://github.com/libbitcoin/libbitcoin-network.git
git clone https://github.com/libbitcoin/libbitcoin-node.git
git clone https://github.com/libbitcoin/libbitcoin-protocol.git
git clone https://github.com/libbitcoin/libbitcoin-server.git

REM Download the gsl dependency manually from 
REM https://github.com/imatix/gsl/releases/download/NuGet-4.1.0.1/gsl.exe.
REM Copy the gsl.exe manually to the libbitcoin-build folder in your work 
REM directory. 

REM Run the libbitcoin-build generation script.
REM Newly generated build files are copied to the cloned repos.
cd libbitcoin-build
./generate.cmd
```
