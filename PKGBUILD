# Maintainer: @HydroH <https://github.com/hydroh>

# Archlinux credits:
# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Maintainer: Fabian Bornschein <fabiscafe@archlinux.org>
# Contributor: Ionut Biru <ibiru@archlinux.org>
# Contributor: Michael Kanis <mkanis_at_gmx_dot_de>

# Patch credits:
# https://gitlab.gnome.org/GNOME/mutter/-/merge_requests/3567/
# Author: Jonas Dreßler <verdre@v0yd.nl>
# Author: Jonas Ådahl <jadahl@gmail.com>

pkgname=mutter-xwayland-scaling
pkgver=46.3.1
pkgrel=1
pkgdesc="Window manager and compositor for GNOME with Xwayland fractional scaling patch"
url="https://gitlab.gnome.org/GNOME/mutter"
arch=(x86_64)
license=(GPL-2.0-or-later)
depends=(
  at-spi2-core
  cairo
  colord
  dconf
  fontconfig
  fribidi
  gcc-libs
  gdk-pixbuf2
  glib2
  glibc
  gnome-desktop-4
  gnome-settings-daemon-xwayland-scaling
  graphene
  gsettings-desktop-schemas
  gtk4
  harfbuzz
  iio-sensor-proxy
  lcms2
  libcanberra
  libcolord
  libdisplay-info
  libdrm
  libei
  libglvnd
  libgudev
  libice
  libinput
  libpipewire
  libsm
  libsysprof-capture
  libwacom
  libx11
  libxau
  libxcb
  libxcomposite
  libxcursor
  libxdamage
  libxext
  libxfixes
  libxi
  libxinerama
  libxkbcommon
  libxkbcommon-x11
  libxkbfile
  libxrandr
  libxtst
  mesa
  pango
  pipewire
  pixman
  python
  startup-notification
  systemd-libs
  wayland
  xorg-xwayland
)
makedepends=(
  egl-wayland
  gi-docgen
  git
  glib2-devel
  gobject-introspection
  meson
  sysprof
  wayland-protocols
)
provides=(mutter=$pkgver libmutter-14.so)
conflicts=(mutter)
source=(
  # Mutter tags use SSH signatures which makepkg doesn't understand
  "git+$url.git#tag=${pkgver/[a-z]/.&}"
  "xwayland-scaling.patch"
)
b2sums=('7d9041df986220470c287fe65194ec6e4da8f15540140fb7e0c3fddc95ce6e9ec9fd4f691ed349a31af28e903c769c97d9817ac65c3cc424b002e095cf559606'
        'e1ff0bdf8fa02a612529a399441a5e8c66e2dd8c501619cc4d28dd9df2c748531be9299297bc40a2bf00d00e4e77c700053a4627ba07bbcbb06ef77dee9f91b5')

prepare() {
  cd mutter
  
  patch -p1 -N -i "${srcdir}/xwayland-scaling.patch"
}

build() {
  local meson_options=(
    -D docs=false
    -D egl_device=true
    -D installed_tests=false
    -D libdisplay_info=enabled
    -D tests=false
    -D wayland_eglstream=true
  )

  CFLAGS="${CFLAGS/-O2/-O3} -fno-semantic-interposition"
  LDFLAGS+=" -Wl,-Bsymbolic-functions"

  arch-meson mutter build "${meson_options[@]}"
  meson compile -C build
}

package() {
  meson install -C build --destdir "$pkgdir"
}
