# Maintainer: willemw <willemw12@gmail.com>

_targets="common qt4"
_pkgname=backintime-qt4
pkgname=$_pkgname-bzr
pkgver=r936
pkgrel=1
#pkgdesc="Simple backup/snapshot system inspired by Flyback and TimeVault"
pkgdesc="Simple backup/snapshot system inspired by Flyback and TimeVault ('experimental' development branch)"
url="http://backintime.le-web.org"
license=('GPL')
arch=('any')
depends=('rsync' 'openssh' 'python-dbus'
         'libnotify' 'python-pyqt4')
#         'gksu' 'kdesu')
optdepends=('cron: scheduled backups'
            'encfs: encrypted filesystems'
            'gksu: run as root' 'kdesu: run as root'
            'meld: diff tool' 'kompare: diff tool'
            'pm-utils: power management status check'
            'python-keyring: store passwords' 'python-secretstorage: store passwords'
            'sshfs: remote filesystems')
makedepends=('bzr')
provides=(backintime $_pkgname)
conflicts=(backintime $_pkgname
           backintime-gnome backintime-gtk backintime-kde4)     # backintime reverse dependency conflicts
#source=($pkgname::bzr+https://code.launchpad.net/~bit-team/backintime/trunk)
source=($pkgname::bzr+https://code.launchpad.net/~bit-team/backintime/Qt4)
md5sums=('SKIP')

pkgver() {
  cd $pkgname
  printf "r%s" "$(bzr revno)"
}

prepare() {
  cd $pkgname
  sed -i "s|^Name=Back In Time (root)$|Name=Back In Time (root, gksu)|" qt4/backintime-gnome-root.desktop
  sed -i "s|^Name=Back In Time (root)$|Name=Back In Time (root, kdesu)|" qt4/backintime-kde4-root.desktop
}

build() {
  for i in $_targets; do
    cd "$srcdir/$pkgname/$i"
    ./configure --gksu --kdesu --python3
    make 
  done
}

package() {
  for i in $_targets; do
    cd "$srcdir/$pkgname/$i"
    make DESTDIR="$pkgdir" install 
  done
}

