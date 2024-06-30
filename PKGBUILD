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
pkgver=46.3
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
b2sums=('b228db453c22a94783ceed71eb9489117e0576293f6daa37b7f20b6992b80ee4e67ebeee3b1cf474d306d2341e8d0e26b16820cec9d6c53132ddc7ffd4157634'
        '4eaf9ecc54e7cb876990aed7f4afc7e199e40a20b0268bb2b26e97a980787a234b4ed4f15de5ef620d10e9dbc51d75a967820c516cdf28f09b5db20196e965e9')

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
