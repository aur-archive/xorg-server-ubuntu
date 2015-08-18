# Maintainer: Xiao-Long Chen <chenxiaolong@cxl.epac.to>

pkgbase=xorg-server-ubuntu
pkgname=xorg-server-ubuntu
true && pkgname=('xorg-server-ubuntu' 'xorg-server-xephyr-ubuntu' 'xorg-server-xdmx-ubuntu' 'xorg-server-xvfb-ubuntu' 'xorg-server-xnest-ubuntu' 'xorg-server-common-ubuntu' 'xorg-server-devel-ubuntu')
_ubuntu_rel=0ubuntu3
pkgver=1.11.4.${_ubuntu_rel}
pkgrel=100
arch=('i686' 'x86_64')
license=('custom')
url="http://xorg.freedesktop.org"
makedepends=('pixman' 'libx11' 'mesa' 'libgl' 'xf86driproto' 'xcmiscproto' 'xtrans' 'bigreqsproto' 'randrproto' 'inputproto-ubuntu>=2.1.99.6.1' 'fontsproto' 'videoproto' 'compositeproto' 'recordproto' 'scrnsaverproto' 'resourceproto' 'xineramaproto' 'libxkbfile' 'libxfont' 'renderproto' 'libpciaccess' 'libxv' 'xf86dgaproto' 'libxmu' 'libxrender' 'libxi' 'dmxproto' 'libxaw' 'libdmx' 'libxtst' 'libxres' 'xorg-xkbcomp' 'xorg-util-macros' 'xorg-font-util' 'glproto' 'dri2proto' 'udev' 'libgcrypt' 'fixesproto-ubuntu>=5.0.2ubuntu1' 'libxfixes-ubuntu')
options=('!libtool')
source=("${url}/releases/individual/xserver/${pkgbase%-*}-${pkgver%.*}.tar.bz2"
        "https://launchpad.net/ubuntu/+archive/primary/+files/${pkgbase%-*}_${pkgver%.*}-${_ubuntu_rel}.diff.gz"
        'xvfb-run'
        'xvfb-run.1'
        '10-quirks.conf')
sha512sums=('29013ffd51ff1b6a2b5679580c490d68dc5feaebdc9201a2812a410761200f5468de76c8791ab089950504be649e61f2cccb705587fde66eef1bcd3461f537ed'
            'c7bfb6d3a49600d95c9efe8bfb172bc1367ae50c55f77fa63ac63277a7944cbb65faeb6e55ca0f362034460b5c1d95b80bf9cd5439e5cff15954584cb3b79df8'
            'ca1cda27016f7c269cbdecc45da36255afeef5c1973cc484544f9dfbf56ed1868365c93a4c7f93e3a23e5322f084ec0cdd137e15b43872aae7f0c03040028ce6'
            'de5e2cb3c6825e6cf1f07ca0d52423e17f34d70ec7935e9dd24be5fb9883bf1e03b50ff584931bd3b41095c510ab2aa44d2573fd5feaebdcb59363b65607ff22'
            '9a1a5568be751435daea720cfc4bad209d62545cc10ea2f49113c41669c8130809a680492256ef331757fe8539d2e0e5e9e67a36f7c48c8d92d9b3e957d28fa2')

# AUR fix
pkgdesc="Xorg X server with Ubuntu's patches"

build() {
  cd "${srcdir}/${pkgbase%-*}-${pkgver%.*}"

  # Apply Ubuntu patches
  patch -Np1 -i "${srcdir}/${pkgbase%-*}_${pkgver%.*}-${_ubuntu_rel}.diff"

  for i in $(cat debian/patches/series | grep -v '#'); do
    patch -Np1 -i "debian/patches/${i}"
  done

  ./autogen.sh \
    `# enable features` \
    --enable-aiglx \
    --enable-composite \
    --enable-config-udev \
    --enable-dbe \
    --enable-dga \
    --enable-dmx \
    --enable-dpms \
    --enable-dri \
    --enable-dri2 \
    --enable-gestures \
    --enable-glx \
    --enable-ipv6 \
    --enable-glx-tls \
    --enable-kdrive \
    --enable-mitshm \
    --enable-record \
    --enable-registry \
    --enable-screensaver \
    --enable-xace \
    --enable-xcsecurity \
    --enable-xdm-auth-1 \
    --enable-xdmcp \
    --enable-xephyr \
    --enable-xf86vidmode \
    --enable-xfbdev \
    --enable-xfree86-utils \
    --enable-xinerama \
    --enable-xnest \
    --enable-xorg \
    --enable-xres \
    --enable-xv \
    --enable-xvfb \
    --enable-xvmc \
    `# disable features` \
    --disable-config-dbus \
    --disable-config-hal \
    --disable-debug \
    --disable-devel-docs \
    --disable-dtrace \
    --disable-install-libxf86config \
    --disable-install-setuid \
    --disable-silent-rules \
    --disable-static \
    --disable-strict-compilation \
    --disable-tslib \
    --disable-xcalibrate \
    --disable-xf86bigfont \
    --disable-xfake \
    --disable-xquartz \
    --disable-xselinux \
    --disable-xwin \
    `# installation prefixes and paths` \
    --localstatedir=/var \
    --prefix=/usr \
    --sysconfdir=/etc/X11 \
    --with-fontrootdir=/usr/share/fonts \
    --with-xkb-output=/var/lib/xkb \
    --with-xkb-path=/usr/share/X11/xkb \
    `# configuration options` \
    --with-default-xkb-rules=evdev \
    --with-fop=no `# build fix` \
    --with-int10=x86emu \
    --with-sha1=libgcrypt

  # Build fix
  #find . -name Makefile -exec \
  #  sed -i \
  #    -e 's/-Werror=int-to-pointer-cast//g' \
  #    -e 's/-Werror=address//g' \
  #    -e 's/-Werror=array-bounds//g' \
  #    -e 's/-Werror=attributes//g' \
  #    -e 's/-Werror=clobbered//g' \
  #    -e 's/-Werror=format-security//g' \
  #    -e 's/-Werror=implicit//g' \
  #    -e 's/-Werror=incompatible-pointer-types//g' \
  #    -e 's/-Werror=init-self//g' \
  #    -e 's/-Werror=int-to-pointer-cast//g' \
  #    -e 's/-Werror=main//g' \
  #    -e 's/-Werror=missing-braces//g' \
  #    -e 's/-Werror=nonnull//g' \
  #    -e 's/-Werror=return-type//g' \
  #    -e 's/-Werror=sequence-point//g' \
  #    -e 's/-Werror=trigraphs//g' \
  #    -e 's/-Werror=unknown-warning-option//g' \
  #    -e 's/-Werror=unused-command-line-argument//g' \
  #    -e 's/-Wformat-nonliteral//g' \
  #    -e 's/-Wimplicit-function-declaration//g' \
  #    -e 's/-Wparentheses//g' \
  #    -e 's/-Werror=write-strings//g' \
  #    -e 's/-Werror=pointer-to-int-cast//g' \
  #    {} \;
    
  make ${MAKEFLAGS}

  # Disable subdirs for make install rule to make splitting easier
  sed -e 's/^DMX_SUBDIRS =.*/DMX_SUBDIRS =/' \
      -e 's/^XVFB_SUBDIRS =.*/XVFB_SUBDIRS =/' \
      -e 's/^XNEST_SUBDIRS =.*/XNEST_SUBDIRS = /' \
      -e 's/^KDRIVE_SUBDIRS =.*/KDRIVE_SUBDIRS =/' \
      -i hw/Makefile
}

package_xorg-server-common-ubuntu() {
  pkgdesc="Xorg server common files"
  depends=('xkeyboard-config' 'xorg-xkbcomp' 'xorg-setxkbmap' 'xorg-fonts-misc')
  provides=('xorg-server-common')
  conflicts=('xorg-server-common' 'qt-ubuntu<4.8.0.1ubuntu2' 'utouch-frame<2.1.0')

  cd "${srcdir}/${pkgbase%-*}-${pkgver%.*}"
  install -m755 -d "${pkgdir}/usr/share/licenses/xorg-server-common"
  install -m644 COPYING "${pkgdir}/usr/share/licenses/xorg-server-common"
  
  make -C xkb DESTDIR="${pkgdir}" install-data

  install -m755 -d "${pkgdir}/usr/share/man/man1"
  install -m644 man/Xserver.1 "${pkgdir}/usr/share/man/man1/"

  install -m755 -d "${pkgdir}/usr/lib/xorg"
  install -m644 dix/protocol.txt "${pkgdir}/usr/lib/xorg/"
}

package_xorg-server-ubuntu() {
  pkgdesc="Xorg X server"
  depends=('libxdmcp' 'libxfont' 'udev' 'libpciaccess' 'libdrm' 'pixman' 'libgcrypt' 'libxau' 'xorg-server-common-ubuntu')
  #Cannot put xf86-input-evdev-ubuntu in the dependencies - the AUR will
  # cause a dependency loop due to the order the packages are installed
  backup=('etc/X11/xorg.conf.d/10-evdev.conf' 'etc/X11/xorg.conf.d/10-quirks.conf')
  provides=('x-server' 'xorg-server')
  conflicts=('xorg-server')
  groups=('xorg')

  cd "${srcdir}/${pkgbase%-*}-${pkgver%.*}"
  make DESTDIR="${pkgdir}" install

  install -m755 -d "${pkgdir}/etc/X11"
  mv "${pkgdir}/usr/share/X11/xorg.conf.d" "${pkgdir}/etc/X11/"
  install -m644 "${srcdir}/10-quirks.conf" "${pkgdir}/etc/X11/xorg.conf.d/"

  # Some Debian stuff
    # This should be done by evdev
  #install -m644 "debian/local/10-kbd.conf" "${pkgdir}/etc/X11/xorg.conf.d/"
  #install -m644 "debian/local/10-mouse.conf" "${pkgdir}/etc/X11/xorg.conf.d/"
  install -dm755 "${pkgdir}/lib/udev/"
  install -m644 'debian/local/64-xorg-xkb.rules' "${pkgdir}/lib/udev/"

  rmdir "${pkgdir}/usr/share/X11"

  # Needed for non-mesa drivers, libgl will restore it
  mv "${pkgdir}/usr/lib/xorg/modules/extensions/libglx.so" \
     "${pkgdir}/usr/lib/xorg/modules/extensions/libglx.xorg"

  rm -rf "${pkgdir}/var"

  rm -f "${pkgdir}/usr/share/man/man1/Xserver.1"
  rm -f "${pkgdir}/usr/lib/xorg/protocol.txt"

  install -m755 -d "${pkgdir}/usr/share/licenses/xorg-server"
  ln -sf ../xorg-server-common/COPYING "${pkgdir}/usr/share/licenses/xorg-server/COPYING"

  rm -rf "${pkgdir}/usr/lib/pkgconfig"
  rm -rf "${pkgdir}/usr/include"
  rm -rf "${pkgdir}/usr/share/aclocal"
}

package_xorg-server-xephyr-ubuntu() {
  pkgdesc="A nested X server that runs as an X application"
  depends=('libxfont' 'libgl' 'libgcrypt' 'libxv' 'pixman' 'xorg-server-common-ubuntu')
  provides=('xorg-server-xephyr')
  conflicts=('xorg-server-xephyr')

  cd "${srcdir}/${pkgbase%-*}-${pkgver%.*}/hw/kdrive"
  make DESTDIR="${pkgdir}" install

  install -m755 -d "${pkgdir}/usr/share/licenses/xorg-server-xephyr"
  ln -sf ../xorg-server-common/COPYING "${pkgdir}/usr/share/licenses/xorg-server-xephyr/COPYING"
}

package_xorg-server-xvfb-ubuntu() {
  pkgdesc="Virtual framebuffer X server"
  depends=('libxfont' 'libxdmcp' 'libxau' 'libgcrypt' 'pixman' 'xorg-server-common-ubuntu')
  provides=('xorg-server-xvfb')
  conflicts=('xorg-server-xvfb')

  cd "${srcdir}/${pkgbase%-*}-${pkgver%.*}/hw/vfb"
  make DESTDIR="${pkgdir}" install

  install -m755 "${srcdir}/xvfb-run" "${pkgdir}/usr/bin/"
  install -m644 "${srcdir}/xvfb-run.1" "${pkgdir}/usr/share/man/man1/"

  install -m755 -d "${pkgdir}/usr/share/licenses/xorg-server-xvfb"
  ln -sf ../xorg-server-common/COPYING "${pkgdir}/usr/share/licenses/xorg-server-xvfb/COPYING"
}

package_xorg-server-xnest-ubuntu() {
  pkgdesc="A nested X server that runs as an X application"
  depends=('libxfont' 'libxext' 'libgcrypt' 'pixman' 'xorg-server-common-ubuntu')
  provides=('xorg-server-xnest')
  conflicts=('xorg-server-xnest')

  cd "${srcdir}/${pkgbase%-*}-${pkgver%.*}/hw/xnest"
  make DESTDIR="${pkgdir}" install

  install -m755 -d "${pkgdir}/usr/share/licenses/xorg-server-xnest"
  ln -sf ../xorg-server-common/COPYING "${pkgdir}/usr/share/licenses/xorg-server-xnest/COPYING"
}

package_xorg-server-xdmx-ubuntu() {
  pkgdesc="Distributed Multihead X Server and utilities"
  depends=('libxfont' 'libxi' 'libgcrypt' 'libxaw' 'libxrender' 'libdmx' 'libxfixes' 'pixman' 'xorg-server-common-ubuntu')
  provides=('xorg-server-xdmx')
  conflicts=('xorg-server-xdmx')

  cd "${srcdir}/${pkgbase%-*}-${pkgver%.*}/hw/dmx"
  make DESTDIR="${pkgdir}" install

  install -m755 -d "${pkgdir}/usr/share/licenses/xorg-server-xdmx"
  ln -sf ../xorg-server-common/COPYING "${pkgdir}/usr/share/licenses/xorg-server-xdmx/COPYING"
}

package_xorg-server-devel-ubuntu() {
  pkgdesc="Development files for the X.Org X server"
  depends=('xproto' 'randrproto' 'renderproto' 'xextproto' 'inputproto-ubuntu' 'kbproto' 'fontsproto' 'videoproto' 'dri2proto' 'xineramaproto' 'xorg-util-macros' 'pixman' 'libpciaccess')
  provides=('xorg-server-devel')
  conflicts=('xorg-server-devel')

  cd "${srcdir}/${pkgbase%-*}-${pkgver%.*}"
  make DESTDIR="${pkgdir}" install

  rm -rf "${pkgdir}/usr/bin"
  rm -rf "${pkgdir}/usr/share/man"
  rm -rf "${pkgdir}/usr/share/doc"
  rm -rf "${pkgdir}/usr/share/X11"
  rm -rf "${pkgdir}/usr/lib/xorg"
  rm -rf "${pkgdir}/var"

  install -m755 -d "${pkgdir}/usr/share/licenses/xorg-server-devel"
  ln -sf ../xorg-server-common/COPYING "${pkgdir}/usr/share/licenses/xorg-server-devel/COPYING"
}
