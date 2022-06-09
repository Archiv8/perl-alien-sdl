#!/bin/bash

# Based on the original packaging by  Marcell Meszaros < marcell.meszaros AT runbox.eu > Jan Alexander Steffens (heftig) <heftig@archlinux.org> Allan McRae <allan@archlinux.org> and Sarah Hay <sarahhay@mb.sympatico.ca>

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# ToDo: Add files: User documentation
# ToDo: Add files: Tooling
# FixMe: Namcap warnings and errors

# Maintainer: Ross Clark <https://github.com/Archiv8/perl-cddb/discussions>
# Contributor: Ross Clark <https://github.com/Archiv8/perl-cddb/discussions>

# This package must not be "any" arch.
# The Build.PL script's "--with-sdl-config" acquires arch-specific library paths
# from the installed SDL instance, and puts that into the created package.
# Requires rebuild with every arch/config change in the provided SDL package.

_relname="Alien-SDL"

pkgname="perl-alien-sdl"
pkgver=1.446
pkgrel=13
pkgdesc="Build, find and use SDL binaries (package is specific to architecture and SDL package used at build-time)"
arch=(
  "$CARCH"
  )
license=(
  "GPL"
  )
url="https://metacpan.org/dist/Alien-SDL"
depends=(
  "perl>=5.008"
  "perl-capture-tiny"
  "perl-extutils-cbuilder"
  "perl-file-sharedir>=1.00"
  "perl-file-temp"
  "perl-pathtools"
  "sdl12-compat"
)
makedepends=(
  "perl-archive-extract"
  "perl-archive-tar"
  "perl-archive-zip"
  "perl-digest-sha"
  "perl-file-fetch>=0.24"
  "perl-file-path>=2.08"
  "perl-file-which"
  "perl-module-build>=0.36"
  "perl-text-patch>=1.4"
)
options=(
  "!emptydirs"
  )
source=(
  "https://cpan.metacpan.org/authors/id/F/FR/FROGGS/${_relname}-${pkgver}.tar.gz"
  )
sha512sums=(
  "dfb5f104f449857b9567ca93a0c3b15aed2618e27019569c95c4b7469e1f7d5cc390fe2dda9c6add41e9648c1f6efe053d08a4bd0fcc5bc546a217721bea824c"
)

prepare() {

  cd "${_relname}-${pkgver}"

  # Workaround bug with --with-sdl-config
  sed -i '/^GetOptions/d' Build.PL
}

build() {
  cd "${_relname}-${pkgver}"

  # install module in vendor directories
  perl Build.PL --with-sdl-config
  perl Build
}

package() {
  cd "${_relname}-${pkgver}"
  perl Build install installdirs=vendor destdir="${pkgdir}"
}
