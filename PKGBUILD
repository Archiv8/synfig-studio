#!/bin/bash

# Based on original packaging by Popolon <popolon@popolon.org>, Piernov <piernov@piernov.org>, Sergej Pupykin <pupykin.s+arch@gmail.com> and Franco Iacomella <yaco@gnu.org>

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# [ToDo]: Add files: User documentation
# [ToDo]: Add files: Tooling
# [FixMe]: Namcap warnings and errors

# Maintainer: Ross Clark <https://github.com/Archiv8/synfig-studio/discussions>
# Contributor: Ross Clark <https://github.com/Archiv8/synfig-studio/discussions>

#_langname=""
_relname="synfig"
_partname="studio"
#_cvsname=""

# pkgbase=
pkgname="${_relname}-${_partname}"
pkgver=1.5.1
pkgrel=1
# epoch=
pkgdesc="Open-source 2D Animation Software. Core package providing a GUI to Synfig core"
arch=(
  "x86_64"
)
url="https://www.synfig.org/"
license=(
  "GPL2"
)
# groups=()
depends=(
  "python"
  "gtkmm3"
  "synfig-core>=${pkgver}"
  "sdl_image"

)
# optdepends=()
makedepends=(
  "openexr"
  "imagemagick"
  "xorg-fonts-100dpi"
  "xorg-fonts-75dpi"
  "xorg-fonts-misc"
  "xorg-fonts-type1"
  "intltool"
  "etl>=${pkgver}"
)
# checkdepends=()
provides=(
  "synfigstudio"
)
conflicts=(
  "synfigstudio"
  "synfigstudio-dev"
  "synfigstudio-git"
)
replaces=(
  "synfigstudio"
  "synfigstudio-dev"
  "synfigstudio-git"
)
# backup=()
# options=()
# install=
# changelog=
source=(
  "${_relname}-${pkgver}.tar.gz::https://github.com/${_relname}/${_relname}/archive/v${pkgver}.tar.gz"
)
# noextract=()
# validpgpkeys=()
sha512sums=(
  "0c1dd53a445f037bcdb742d7c17d1d3a2039e80d3e49f5cd67119fb9792d96b47154874d5be42d36443b0d09c61b7864dfe33ebd5f3998783c54eb3cc936d11b"
)

prepare() {

  # Change to the Synfig ETL directory
  cd "${srcdir}/${_relname}-${pkgver}/${pkgname}"

  # Bootstrap as not installing using scripts at project root, i.e, ./1-setup-linux-native.sh, 2-build-production.sh
  ./bootstrap.sh

  # Run configure script
  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc/synfig \
    --enable-jack \
    --disable-update-mimedb
}

build() {
  cd "$srcdir"/synfig-$pkgver/synfig-studio
  export PKG_CONFIG_PATH=/usr/lib/ffmpeg0.10/pkgconfig:/usr/lib/imagemagick6/pkgconfig:$PKG_CONFIG_PATH
  LDFLAGS="$LDFLAGS -Wl,-rpath -Wl,/usr/lib/ffmpeg0.10"
  CFLAGS="$CFLAGS -D__STDC_CONSTANT_MACROS"
  CXXFLAGS="$CXXFLAGS -D__STDC_CONSTANT_MACROS -std=gnu++11"
  [ -f configure ] || { libtoolize --ltdl --copy --force && autoreconf --install --force; }
  intltoolize --force
  [ -f Makefile ] || ./configure --prefix=/usr --sysconfdir=/etc --with-libavcodec --with-libdv
  #  sed -i 's#Gtk::IconSize::IconSize#Gtk::IconSize#' src/gui/dialogs/dialog_color.cpp
  # please pay attention to your number of cores and ram amount for avoid oom errors
  # this number its fine for and amd fx 8350 with 16gb ram
  # you need 2gb per core  for avoid surprises, OR dont do anything while it compiles
  make -j8
}

# check() {}

package() {

  cd "$srcdir"/synfig-$pkgver/synfig-studio
  make DESTDIR="$pkgdir" install
  rm -f "$pkgdir"/usr/share/pixmaps/synfigstudio/*.mng
  install -Dm644 -t "$pkgdir"/usr/share/pixmaps/synfigstudio/ images/*.png
  rm -f "$pkgdir"/usr/share/mime/XMLnamespaces
  rm -f "$pkgdir"/usr/share/mime/aliases
  rm -f "$pkgdir"/usr/share/mime/generic-icons
  rm -f "$pkgdir"/usr/share/mime/globs
  rm -f "$pkgdir"/usr/share/mime/globs2
  rm -f "$pkgdir"/usr/share/mime/icons
  rm -f "$pkgdir"/usr/share/mime/magic
  rm -f "$pkgdir"/usr/share/mime/mime.cache
  rm -f "$pkgdir"/usr/share/mime/subclasses
  rm -f "$pkgdir"/usr/share/mime/treemagic
  rm -f "$pkgdir"/usr/share/mime/types
  rm -f "$pkgdir"/usr/share/mime/version
}
