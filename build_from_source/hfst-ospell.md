Build hfst-ospell from source
=============================
HFST spell checker library and command line tool.

The library is licenced under Apache licence version 2, other licences can be
obtained from University of Helsinki.

Source repo: [hfst-ospell](https://github.com/hfst/hfst-ospell)

Pre-requisites
--------------
### Windows OS:
* [MSYS2](https://www.msys2.org/)
* libxml++2 (pacman -S mingw-w64-x86_64-libxml++2.6)
* libarchive (pacman -S mingw-w64-x86_64-libarchive)
* icu-devel (pacman -S icu-devel)

```shell
[make distclean]
autoreconf -i -v
./configure --enable-hfst-ospell-office=no
make
make install
```
