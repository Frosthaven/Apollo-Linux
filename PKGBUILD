# Maintainer: Frosthaven <noreply@github.com>
# Cosmic-Apollo - COSMIC-tuned Apollo game streaming host with virtual display support

pkgname=cosmic-apollo-linux
pkgver=0.1.0
pkgrel=1
pkgdesc="COSMIC-tuned Apollo game streaming host with virtual display support"
arch=('x86_64')
url='https://github.com/Frosthaven/Cosmic-Apollo-Linux'
license=('GPL-3.0-only')
install=apollo.install

depends=(
  'avahi'
  'curl'
  'evdi'
  'libayatana-appindicator'
  'libcap'
  'libdrm'
  'libevdev'
  'libnotify'
  'libpulse'
  'libva'
  'libx11'
  'libxcb'
  'libxfixes'
  'libxrandr'
  'libxtst'
  'miniupnpc'
  'numactl'
  'openssl'
  'opus'
  'udev'
)

optdepends=(
  'cuda: NVIDIA GPU encoding support'
  'libva-mesa-driver: AMD GPU encoding support'
)

# Take over from upstream Apollo (AUR's `apollo` package) and Sunshine.
# - conflicts: pacman refuses to install either alongside this.
# - replaces:  pacman offers to swap an existing apollo/sunshine for cosmic-apollo-linux on first install.
# - provides:  satisfies any other AUR package that declares `apollo` or `sunshine` as a dep.
provides=('apollo' 'sunshine')
conflicts=('apollo' 'sunshine')
replaces=('apollo' 'sunshine')

# Usar o build local já compilado
source=()
sha256sums=()

package() {
    # Copiar do build debug
    cd "${startdir}"
    
    # Executável
    install -Dm755 "cmake-build-debug/sunshine" "${pkgdir}/usr/bin/apollo"
    
    # Assets
    install -dm755 "${pkgdir}/usr/share/apollo"
    cp -r cmake-build-debug/assets/* "${pkgdir}/usr/share/apollo/"
    
    # Ícones
    install -Dm644 "apollo.svg" "${pkgdir}/usr/share/icons/hicolor/scalable/apps/apollo.svg"
    install -Dm644 "apollo.svg" "${pkgdir}/usr/share/icons/hicolor/scalable/status/apollo-tray.svg"
    install -Dm644 "src_assets/common/assets/web/public/images/apollo-playing.svg" \
        "${pkgdir}/usr/share/icons/hicolor/scalable/status/apollo-playing.svg"
    install -Dm644 "src_assets/common/assets/web/public/images/apollo-pausing.svg" \
        "${pkgdir}/usr/share/icons/hicolor/scalable/status/apollo-pausing.svg"
    install -Dm644 "src_assets/common/assets/web/public/images/apollo-locked.svg" \
        "${pkgdir}/usr/share/icons/hicolor/scalable/status/apollo-locked.svg"
    
    # Udev rules
    install -Dm644 "src_assets/linux/misc/60-sunshine.rules" \
        "${pkgdir}/usr/lib/udev/rules.d/60-apollo.rules"
    
    # Systemd service
    install -Dm644 "cmake-build-debug/sunshine.service" \
        "${pkgdir}/usr/lib/systemd/user/apollo.service"
    
    # Desktop file
    install -Dm644 "cmake-build-debug/dev.lizardbyte.app.Sunshine.desktop" \
        "${pkgdir}/usr/share/applications/apollo.desktop"
    
    # Modificar desktop file
    sed -i 's/sunshine/apollo/g; s/Sunshine/Apollo/g' \
        "${pkgdir}/usr/share/applications/apollo.desktop"
}
