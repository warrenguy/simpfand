# Maintainer: Hong Shick Pak  hongshick.pak@gmail.com

pkgname=simpfand
pkgver=20120925
pkgrel=1
pkgdesc="A simple fan control daemon for ThinkPads"
arch=('i686' 'x86_64')
url="http://github.com/hspasta/simpfand"
license=('GNU3')
depends=('' )
makedepends=('git')
conflicts=('')
provides=('simpfand')

_gitroot="git://github.com/hspasta/simpfand.git"
_gitname="simpfand"

build() {
  msg "Connecting to GIT server...."

  if [[ -d $_gitname ]] ; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_gitname-build"
  cp -r "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  make
}

package() {
  make -C "$srcdir/$_gitname-build" PREFIX=/usr DESTDIR="$pkgdir" install

  install -D -m644 "$srcdir/simpfand.systemd" "$pkgdir/usr/lib/systemd/system/simpfand.service"
}

# vim: ft=sh syn=sh et