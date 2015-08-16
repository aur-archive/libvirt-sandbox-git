# Maintainer: Ansgar Taflinski <ataflinski@uni-koblenz.de>
pkgname=libvirt-sandbox-git
pkgver=20121012
pkgrel=2
pkgdesc="An extension to libvirt which allows sandboxing on top of qemu/KVM and LXC. Git Version"
arch=(i686 x86_64)
url="http://www.libvirt.org"
license=('GPL')
install=libvirt-sandbox.install
makedepends=('git' 'automake')
depends=('libvirt-glib>=0.0.9' 'glib2>=2.28.0' 'libvirt>=0.9.13' 'cpio' 'selinux-usr-libselinux')
provides=('libvirt-sandbox')
conflicts=('libvirt-sandbox')
_gitroot='git://libvirt.org/libvirt-sandbox.git'
_gitname='libvirt-sandbox'
build() {
  msg "Connecting to GIT server...."
  
  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi
  msg "GIT checkout done or server timeout"
  msg "Starting make..."
  rm -rf "$srcdir"/$_gitname-build
  mkdir "$srcdir"/$_gitname-build
  cd "$srcdir/"$_gitname && ls -A1 --indicator-style=none | grep -v "^.git" | xargs -d '\n' cp -r -t ../$_gitname-build # do not copy over the .git folder
  cd "$srcdir"/$_gitname-build
  #cd $srcdir/$pkgname-$pkgver
  aclocal
  autoconf
  ./autogen.sh --prefix=/usr --sysconfdir=/etc
  make
}
package() {
  cd "$srcdir/"$_gitname-build
  make DESTDIR=$pkgdir install
}
