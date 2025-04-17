pkgname=ath11k-suspend-workaround
pkgver=1.0
pkgrel=1
pkgdesc="Workaround for ath11k_pci suspend/resume issues on Lenovo ThinkPad T14s Gen 4"
url="https://wiki.archlinux.org/title/Lenovo_ThinkPad_T14s_(AMD)_Gen_3#Network_/_Wi-Fi"
arch=('any')
license=('MIT')
depends=()
source=('ath11k-suspend.service' 'ath11k-resume.service')
sha256sums=(
  'e0b7be8e5807749987ab5180a108a250a06c5285313aa7773602f93243ace593'
  '51b0e6103418737be3604d91dba4aced5491fcd8e6e4a6e413e8e7aef065bfe6'
)

package() {
  install -Dm644 "$srcdir/ath11k-suspend.service" "$pkgdir/etc/systemd/system/ath11k-suspend.service"
  install -Dm644 "$srcdir/ath11k-resume.service" "$pkgdir/etc/systemd/system/ath11k-resume.service"
}

post_install() {
  systemctl enable ath11k-suspend.service
  systemctl enable ath11k-resume.service
  systemctl start ath11k-suspend.service
  systemctl start ath11k-resume.service

  if systemctl list-unit-files --type=service | grep -q '^NetworkManager.service'; then
    systemctl restart NetworkManager.service
  fi
}

