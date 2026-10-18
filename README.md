# OpenSlide

OpenSlide is a C library for reading whole slide image files (also known as
virtual slides).  It provides a consistent and simple API for reading files
from multiple vendors.


## Features

OpenSlide can read brightfield whole slide images in [several formats][]:

* [Aperio][] (`.svs`)
* [ARGOS][] (`.avs`)
* [DICOM][] (`.dcm`)
* [Hamamatsu][] (`.ndpi`, `.vms`, `.vmu`)
* [Huron][] (`.tif`)
* [Leica][] (`.scn`)
* [MIRAX][] (`.mrxs`)
* [Philips][] (`.tiff`)
* [Sakura][] (`.svslide`)
* [Trestle][] (`.tif`)
* [Ventana][] (`.bif`, `.tif`)
* [Zeiss][] (`.czi`)
* [Generic tiled TIFF][] (`.tif`)

OpenSlide can also provide access to ICC profiles, textual metadata, and
associated images such as a slide label and thumbnail.

[several formats]: https://openslide.org/formats/
[Aperio]: https://openslide.org/formats/aperio/
[ARGOS]: https://openslide.org/formats/argos/
[DICOM]: https://openslide.org/formats/dicom/
[Hamamatsu]: https://openslide.org/formats/hamamatsu/
[Huron]: https://openslide.org/formats/huron/
[Leica]: https://openslide.org/formats/leica/
[MIRAX]: https://openslide.org/formats/mirax/
[Philips]: https://openslide.org/formats/philips/
[Sakura]: https://openslide.org/formats/sakura/
[Trestle]: https://openslide.org/formats/trestle/
[Ventana]: https://openslide.org/formats/ventana/
[Zeiss]: https://openslide.org/formats/zeiss/
[Generic tiled TIFF]: https://openslide.org/formats/generic-tiff/


## Documentation

The [API reference][API] is available on the web, and is also included as
`doc/html/openslide_8h.html` in the source tarball.  [Additional
documentation][docs] is available on the [OpenSlide website][website].

[API]: https://openslide.org/api/openslide_8h.html
[docs]: https://openslide.org/#documentation
[website]: https://openslide.org/


## License

OpenSlide is released under the terms of the [GNU Lesser General Public
License, version 2.1](https://openslide.org/license/).

OpenSlide is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS
FOR A PARTICULAR PURPOSE.  See the GNU Lesser General Public License for
more details.


## Compiling

To build OpenSlide, you will need:

- GCC or Clang
- Meson
- cairo ≥ 1.2
- glib ≥ 2.56
- libdicom ≥ 1.3 (automatically built if missing)
- libjpeg-turbo ≥ 1.3 or libjpeg ≥ 9c
- libpng
- libtiff ≥ 4.0
- libxml2
- OpenJPEG ≥ 2.1
- SQLite ≥ 3.14
- zlib
- Zstandard

Then:

```
meson setup builddir
meson compile -C builddir
meson install -C builddir
```

To build OpenSlide to use within a conda environment, you will need a little tweak as below:

Within the target conda environment:

1. Install `openslide-4.0.x` via `conda install` to simplify dependency installation.
2. Do the following steps:
```
meson setup builddir \
    --prefix "${CONDA_PREFIX}" \
    --pkg-config-path "${CONDA_PREFIX}/lib/pkgconfig:${CONDA_PREFIX}/share/pkgconfig" \
    -Dc_args="-I${CONDA_PREFIX}/include" \
    -Dc_link_args="-Wl,-rpath,'\$ORIGIN/../lib' -Wl,-rpath,${CONDA_PREFIX}/lib -L${CONDA_PREFIX}/lib" \
    --libdir=lib
meson compile -C builddir
meson install -C builddir
```

## Acknowledgements

OpenSlide has been developed by Carnegie Mellon University and other
contributors.

OpenSlide has been supported by the National Institutes of Health and
the Clinical and Translational Science Institute at the University of
Pittsburgh.

Development of DICOM and ICC functionality was supported by NCI Imaging
Data Commons and has been funded in whole or in part with Federal funds
from the National Cancer Institute, National Institutes of Health, under
Task Order No. HHSN26110071 under Contract No. HHSN261201500003l.

## Note for installing dependencies

For Debian, you will need

| Dependency | Package |
| --- | --- |
| cairo | `libcairo2-dev` |
| glib | `libglib2.0-dev` |
| libdicom | **optional** |
| libjpeg-turbo | `libjpeg62-turbo-dev` |
| libpng | `libpng-dev` |
| libtiff | `libtiff-dev` |
| libxml2 | `libxml2-dev` |
| openjpeg | `libopenjp2-7-dev` |
| sqlite | `libsqlite3-dev` |
| zlib | `zlib1g-dev` |
| zstandard | `libzstd-dev` |

| For test | Package |
| --- | --- |
| libjpeg-turbo | `libjpeg-turbo-progs` |
| xdelta3 | `xdelta3` |
| valgrind | `valgrind` |
| clang | `clang` |

For Ubuntu, you will need

| Dependency | Package |
| --- | --- |
| To be | Filled |
