GNU FriBidi 1.0.18, the Unicode Bidirectional Algorithm (UAX #9), for the
layout of Encoding -2 (right-to-left) events in src/subtitles/RTS.cpp.

Source: https://github.com/fribidi/fribidi/releases/download/v1.0.18/fribidi-1.0.18.tar.xz
(SHA-256 1de5e8073d035388b71d0b2d452b1da1f8caeea8a7702997b401fe1b6250727f)

COPYING, AUTHORS and lib/*.c, lib/*.h are the files of that name in the
tarball, unchanged, except:

- lib/fribidi-config.h, written from lib/fribidi-config.h.in for MSVC;
- lib/bidi-type.tab.i and lib/fribidi-unicode-version.h, regenerated from the
  tarball's gen.tab/unidata (Unicode 18.0.0): the copies in the tarball are
  from Unicode 14.0.0. In the extracted tarball, on Linux:

    A="-UHAVE_CONFIG_H -DHAVE_STRINGIZE -DDONT_HAVE_FRIBIDI_CONFIG_H -DHAVE_STDLIB_H -DHAVE_STRING_H"
    cc $A -Ilib gen.tab/gen-unicode-version.c -o gen-unicode-version
    ./gen-unicode-version gen.tab/unidata/ReadMe.txt gen.tab/unidata/BidiMirroring.txt \
        gen-unicode-version > lib/fribidi-unicode-version.h
    cc $A -Ilib gen.tab/gen-bidi-type-tab.c gen.tab/packtab.c -o gen-bidi-type-tab
    ./gen-bidi-type-tab 2 gen.tab/unidata/UnicodeData.txt gen-bidi-type-tab > lib/bidi-type.tab.i

  (the second step must see the new lib/fribidi-unicode-version.h). The bidi
  types then equal those of the system libfribidi 1.0.18 on all code points.

Only fribidi-bidi.c, fribidi-run.c and fribidi-bidi-types.c are built
(fribidi.vcxproj): bidi types, embedding levels and line reordering.

License: GNU Lesser General Public License version 2.1 or later (COPYING).
