# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Maintainer: Gaetan Bisson <bisson@archlinux.org>

pkgname=hostapd-git
pkgver=20230511.cc8a09a48
pkgrel=1
pkgdesc='IEEE 802.11 AP, IEEE 802.1X/WPA/WPA2/EAP/RADIUS Authenticator'
url='http://w1.fi/hostapd/'
arch=('x86_64')
license=('custom')
makedepends=('git')
depends=('openssl' 'libnl')
source=('git://w1.fi/hostap.git' 'config')
sha256sums=('SKIP' 'SKIP')

options=('emptydirs')

conflicts=('hostapd')
provides=('hostapd')

pkgver() {
	cd "${srcdir}/hostap"
	git log -1 --format='%cd.%h' --date=short | tr -d -
}

build() {
	cd "${srcdir}/hostap/hostapd"
	cp "${srcdir}/config" ".config"
	make -j"$(nproc)"
}

package() {
	cd "${srcdir}/hostap/hostapd"

	install -d "${pkgdir}"/usr/bin
	install -t "${pkgdir}"/usr/bin hostapd hostapd_cli

	install -d "${pkgdir}"/usr/share/doc/hostapd
	install -t "${pkgdir}"/usr/share/doc/hostapd -m644 hostapd.[a-z]* wired.conf hlr_auc_gw.milenage_db

	install -d "${pkgdir}"/etc/hostapd
	install -Dm644 hostapd.8 "${pkgdir}"/usr/share/man/man8/hostapd.8
	install -Dm644 hostapd_cli.1 "${pkgdir}"/usr/share/man/man1/hostapd_cli.1
	install -Dm644 ../COPYING "${pkgdir}"/usr/share/licenses/hostapd/COPYING
}
