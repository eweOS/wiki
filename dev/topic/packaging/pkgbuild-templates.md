---
title: PKGBUILD Templates
description: 
published: 1
date: 2024-10-16T07:00:37.004Z
tags: 
editor: markdown
dateCreated: 2023-12-07T03:25:04.800Z
---

# Programming Language

## python

## perl

```
# Maintainer: Your Name <you@example.com>

pkgname=perl-module-name
pkgver=x.xx
pkgrel=1
pkgdesc="DESCR"
arch=('any')
url="https://search.cpan.org/dist/MODULE-NAME"
license=('GPL' 'PerlArtistic')
depends=('perl')
options=('!emptydirs')
source=("https://www.cpan.org/authors/id/perl-module-name.tar.gz")
sha256sums=('SUMS')

build() {
  cd $pkgname-$pkgver
  perl Makefile.PL INSTALLDIRS=vendor
  make
}

check() {
  cd $pkgname-$pkgver
  make test
}

package() {
  cd $pkgname-$pkgver
  make install DESTDIR="$pkgdir"

  find "$pkgdir" -name '.packlist' -delete
  find "$pkgdir" -name '*.pod' -delete
}
```

# Desktop Components

## QT

```
# Maintainer: Your Name <you@example.com>

_comp=COMPNAME
pkgname=qt6-$_comp
_qtver=6.7.0
pkgver=${_qtver/-/}
pkgrel=1
arch=(x86_64 aarch64 riscv64)
url='https://www.qt.io'
license=(GPL3 LGPL3 FDL custom)
pkgdesc='DESCR'
_pkgfn=${pkgname/6-/}-everywhere-src-$_qtver
depends=(qt6-base DEPENDS)
makedepends=(cmake git ninja MAKEDEPENDS)
groups=(qt6)
source=(https://download.qt.io/official_releases/qt/${pkgver%.*}/$_qtver/submodules/$_pkgfn.tar.xz)
sha256sums=('SUMS')

build() {
  export CMARGS=(
    -DCMAKE_INSTALL_PREFIX=/usr
    -DCMAKE_BUILD_TYPE=RelWithDebInfo
    -DCMAKE_MESSAGE_LOG_LEVEL=STATUS
  )

  export DIRARGS=(
    -DINSTALL_BINDIR=lib/qt6/bin
    -DINSTALL_PUBLICBINDIR=usr/bin
    -DINSTALL_LIBEXECDIR=lib/qt6
    -DINSTALL_DOCDIR=share/doc/qt6
    -DINSTALL_ARCHDATADIR=lib/qt6
    -DINSTALL_DATADIR=share/qt6
    -DINSTALL_INCLUDEDIR=include/qt6
    -DINSTALL_MKSPECSDIR=lib/qt6/mkspecs
    -DINSTALL_EXAMPLESDIR=share/doc/qt6/examples
  )

  if check_option lto y; then
    CMARGS+=(-DCMAKE_INTERPROCEDURAL_OPTIMIZATION=ON)
  else
    FEATUREARGS+=(-DFEATURE_ltcg=OFF)
  fi

  cmake -B build -S $_pkgfn -G Ninja \
    "${CMARGS[@]}" \
    "${DIRARGS[@]}"
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build

  # Install symlinks for user-facing tools
  cd "$pkgdir"
  mkdir usr/bin
  while read _line; do
    ln -s $_line
  done < "$srcdir"/build/user_facing_tool_links.txt

  install -d "$pkgdir"/usr/share/licenses
  ln -s /usr/share/licenses/qt6-base "$pkgdir"/usr/share/licenses/$pkgname
}

```

## KDE Framework

```
# Maintainer: Your Name <you@example.com>

_compname=COMPNAME
pkgname=k$_compname
pkgver=6.1.0
pkgrel=1
pkgdesc='DESCR'
arch=(x86_64 aarch64 riscv64)
url='https://community.kde.org/Frameworks'
license=(LGPL-2.0-only LGPL-3.0-only)
depends=(qt6-base DEPS)
makedepends=(extra-cmake-modules qt6-tools MAKEDEPS)
groups=(kf6)
source=(https://download.kde.org/stable/frameworks/${pkgver%.*}/$pkgname-$pkgver.tar.xz)
sha256sums=('SUMS')

build() {
  cmake -B build -S $pkgname-$pkgver \
    -DBUILD_TESTING=OFF
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}
```

## Special

### xvfb-run alternative for wayland:

```
export XDG_RUNTIME_DIR="$PWD/runtime-dir" WAYLAND_DISPLAY=wayland-5

mkdir -p -m 700 "$XDG_RUNTIME_DIR"
weston --backend=headless-backend.so --socket=$WAYLAND_DISPLAY --idle-time=0 &
_w=$!

trap "kill $_w; wait" EXIT
```