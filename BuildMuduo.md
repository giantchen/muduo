# Build Muduo #

## Before building ##
### Platform Supported ###

Linux only.

Main:
  * Ubuntu 10.04 LTS (x86-64 or x86)
  * Debian 6.0 Squeeze (x86-64 or x86)

Secondary:
  * CentOS 6
  * Fedora 13 and later

### Required packages ###
  * CMake >= 2.6
  * g++ 4.x
  * boost >= 1.36
  * Linux kernel >= 2.6.28

To install required packages on Ubuntu/Debian
```
$ sudo apt-get install libboost_VER_-dev cmake g++
```

Optional, install C-ares DNS and Google Protobuf, more examples will be built.
```
$ sudo apt-get install protobuf-compiler libprotobuf-dev libc-ares-dev
```
## Steps to build & install ##

### Download latest source tarball ###

http://code.google.com/p/muduo/downloads/list

### Extract and build ###

```
$ tar zxf muduo-VERSION.tar.gz
$ cd muduo
$ ./build.sh
```
this will build Muduo in `../build/debug` , binaries and libraries are in `bin, lib` respectively.

to build optimized version:
```
$ BUILD_TYPE=release ./build.sh 
```
this will build Muduo in `../build/release` , binaries and libraries are in `bin, lib` respectively.

### Install ###

```
$ ./build.sh install
```

or

```
$ BUILD_TYPE=release ./build.sh install
```

By default, Muduo will be installed to your working directory in your home(../build/debug-install), not the system directory (/usr/local)
```
.
|- muduo  # source directory
|- build       # build directory
   |- debug    # build directory for debug version
   |- release  # build directory for release version
   |- debug-install  # install directory
      |- include     # header files
         |- muduo
      |- lib         # libraries
```

### How to use Muduo as a library ###
You may either use CMake or GNU Make to build your applications with Muduo library.

Examples in
https://github.com/chenshuo/muduo-tutorial

## Next Steps ##

### Check examples in Muduo ###
Muduo has a handful examples, in ` muduo/examples ` http://code.google.com/p/muduo/source/browse/trunk/examples/ .

See MuduoExamples.

### Read the Tutorial ###

See MuduoTutorial.