Build libvoikko from source
=============================
Voikko is a morphological analyzer, spelling and grammar checker, hyphenator and collection of related linguistic data for Finnish language.
Voikko also supports other languages such as Northern Sami but all functionality such as grammar checking may not yet be available for these.

Source repo: [corevoikko](https://github.com/voikko/corevoikko)

Pre-requisites
--------------
### Windows OS:
* [MSYS2](https://www.msys2.org/)
* [hfst-ospell](https://github.com/hfst/hfst-ospell)

```shell
[make distclean]
autoreconf -i -v
./configure
make
make install
```
