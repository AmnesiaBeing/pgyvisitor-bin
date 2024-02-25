# Maintainer: JSpringYC <JSpringYC@gmail.com>

pkgname=pgyvisitor-bin
_pkgname=PgyVisitor
pkgver=6.2.0
pkgrel=1
pkgdesc="Suitable for business personnal long-distance intelligent network access"
arch=('x86_64')
url="https://pgy.oray.com/download/"
license=('custom')
conflicts=('pgyvpn' 'pgyvpn-bin')
install=pgyvisitor-bin.install
source=('LICENSE::https://service.oray.com/question/1820.html'
        "${pkgname%-bin}.service"
        "${_pkgname}_${pkgver}_${arch}.deb::https://pgy.oray.com/softwares/153/download/2156/${_pkgname}_${pkgver}_${arch}.deb")
sha256sums=('SKIP'
            'SKIP'
            'e062a592f1f127fa589f6919b3c6e96b71e403854d22d30d75b2cd753c45f2bc')

package() {
  tar -xf data.tar.*z -C ${pkgdir}

  cd ${pkgdir}

  # binary
  for binary in usr/sbin/*;
  do
    install -Dm755 $binary usr/bin/`basename $binary`
  done
  rm -rf usr/sbin

  # systemd service
  install -Dm644 ${srcdir}/${pkgname%-bin}.service usr/lib/systemd/system/${pkgname%-bin}.service
  if [ $CARCH == 'x86_64' ] || [ $CARCH == 'i686' ];then
    rm -rf etc/init.d
  else
    rm -rf lib
  fi

  # license
  install -Dm644 ${srcdir}/LICENSE usr/share/licenses/${pkgname}/LICENSE

  # fixed permission
  chown -R root:root usr etc
  chmod 755 usr usr/share etc etc/oray etc/oray/pgyvpn
}
