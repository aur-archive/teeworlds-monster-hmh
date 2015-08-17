# Maintainer: josephgbr <rafael.f.f1@gmail.com>

# Compatible with Teeworlds 0.6.2 and 0.6.3

pkgname=teeworlds-monster-hmh
pkgver=1.2
pkgrel=1
pkgdesc="A customized server by HMH with bad monsters"
arch=('i686' 'x86_64')
url="https://github.com/H-M-H/Monster_HMH"
license=('custom')
depends=('teeworlds')
makedepends=('python' 'bam')
provides=('teeworlds-monster')
conflicts=('teeworlds-monster')
source=(https://github.com/H-M-H/Monster_HMH/archive/v$pkgver.tar.gz
        ctf5_easy.map ctf5_monster.map ktm5.map monster_rain.map
        monster_world.map server.sh.in)
md5sums=('be88932fa579475c8da2ef847c40bec4'
         'd4e7a5f167fc96fb4b1755eb72ce705c'
         'cf1b721bd7b75797c331f75b68937ccd'
         '10def7d461d6bb8a83e3bca10e2a002d'
         '237079fe2b633bc8b2e447e5183a407f'
         'c56f4adaeccaab7557840b48c19da013'
         '529146a3b13993770fa414f66c67fa26')

build() {
  cd Monster_HMH-$pkgver
  bam server_release
}

package() {
  cd Monster_HMH-$pkgver
  
  install -Dm755 teeworlds_srv "$pkgdir"/usr/share/$pkgname/teeworlds_srv
  
  install -Dm644 Serverconfig.cfg "$pkgdir"/usr/share/$pkgname/server.cfg
    sed -i '/change_map/d' "$pkgdir"/usr/share/$pkgname/server.cfg
    
  install -Dm755 "$srcdir"/server.sh.in "$pkgdir"/usr/bin/${pkgname}_srv
  sed -i "s/@MODNAME@/$pkgname/" "$pkgdir"/usr/bin/${pkgname}_srv
  
  install -dm755  "$pkgdir"/usr/share/teeworlds/data/maps/
  for map in ctf5_easy ctf5_monster ktm5 monster_rain monster_world; do
    install -Dm644 "$srcdir"/$map.map "$pkgdir/usr/share/teeworlds/data/maps/"
    echo "add_vote $map change_map $map" >> "$pkgdir"/usr/share/$pkgname/server.cfg
  done
}
