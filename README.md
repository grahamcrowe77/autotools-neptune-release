This repo demonstrates a method for making a self contained Erlang release
using GNU Autotools.

This git repo is inspired by:
1. **Autotools 2nd Edition** *A Practitioner's Guide To GNU Autoconf, GNU
   Automake and Libtool* **by John Calcote**
2. **[Romain Lenglet's blog](http://www.berabera.info/2009/08/02/eunit-integration-into-gnu-autotest/)**

Bootstrapping the build system requires the installation of GNU Autotools
(autoconf, automake and libtool).To bootstrap the build system run the
following:
```bash
git clone https://github.com/grahamcrowe77/autotools-neptune-release.git
cd autotools-neptune-release
./bootstrap.sh
```

To test building in the source tree:
```bash
./configure
make
make install DESTDIR=$PWD/inst
make maintainer-clean
```

Linux Distro Erlang installations are usually installed with prefix=/usr. To
ensure the correct installation run configure as follows:
```bash
./configure --prefix=/usr
make
sudo make install
```
