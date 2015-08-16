# Maintainer: BxS <bxsbxs at gmail dot com>

pkgname=microchip-mplab_bin
pkgverbeta=7.12
pkgver=10b$pkgverbeta
pkgrel=7
pkgdesc="IDE for Microchip PIC and dsPIC development a.k.a. MPLAB X"
arch=(i686 x86_64)
url=http://www.microchip.com/en_US/family/mplabx/index.html
license=(custom)
depends=(java-runtime=6 libusb xdg-utils hicolor-icon-theme)
[ $CARCH = x86_64 ] && depends=(${depends[@]} lib32-glibc)
optdepends=('microchip-mplabc18_bin: C compiler for PIC18 MCUs'
            'microchip-mplabc30_bin: C compiler for PIC24 MCUs and dsPIC DSCs'
            'microchip-mplabc32_bin: C Compiler for PIC32 MCUs'
            'hitech-picc_bin: C compiler for PIC10/12/16 MCUs'
            'hitech-picc-18_bin: C compiler for PIC18 MCUs'
            'hitech-dspicc-bin: C Compiler for PIC24 MCUs and dsPIC DSCs'
            'hitech-picc32-bin: C compiler for PIC32 MCUs'
            'sdcc: C compiler for PIC16/18 MCUs')
provides=(mplab)
conflicts=(mplab)
options=(!strip docs libtool emptydirs !zipman)
install=$pkgname.install
user=$USER
instdir=/opt/microchip/mplabx
installer=mplabx-ide-beta$pkgverbeta-linux-installer.run
source=(http://ww1.microchip.com/downloads/mplab/X_Beta/$installer
        z010_mchp_tools.rules
        microchip-mplab.desktop
        microchip-mplab.png
        LICENSE)
md5sums=(2d99c6f001d53d0a02412b80f1ead81f                                                                                                                        
         d11f3d54362d75c03edba2835da933bb
         bf216a43020e038603a29c4ffb1ca92f
         b45656e8e99e213b8151bbafac0a37ac
         2d1c400907ba208d3f06ec1ee84eb2c0)

package() {
  echo -e "Creating Package\n  Please Wait..."

  cd $pkgdir

  mkdir -p $pkgdir$instdir

  echo -e "#! /bin/sh\necho \"java version \\\"1.6\"" > java
  chmod 0755 java
  PATH=$pkgdir:$PATH
  chmod 0755 $srcdir/$installer
  echo -e "\n\n\n\n\n\n\n\n\n\n\n\n\n\n\ny\n\ny\ni\ni\ni\ni\ni\ni\ni\ni\ni\ni\ni\ni\ni\ni\ni\ni\n" > inst_input
  $srcdir/$installer --mode text --installdir $pkgdir$instdir < inst_input &> /dev/null || true
  rm inst_input java

  rm "/home/$user/Desktop/MPLAB X IDE beta$pkgverbeta.desktop" &> /dev/null || true

  rm "$pkgdir$instdir/Uninstall MPLAB X IDE"{," beta$pkgverbeta.desktop"} &> /dev/null || true
  rm -r $pkgdir$instdir/rollbackBackupDirectory &> /dev/null || true

  sed 's/\x2F\x75\x73\x72\x2F\x6C\x6F\x63\x61\x6C\x2F\x6C\x69\x62\x2F\x6C\x69\x62\x6D\x63\x68\x70\x75\x73\x62\x2D\x31\x2E\x30\x2E\x73\x6F\x00/\x6C\x69\x62\x75\x73\x62\x2D\x31\x2E\x30\x2E\x73\x6F\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00/' -i $pkgdir/opt/microchip/mplabx/mplab_ide/mplablibs/modules/lib/libUSBAccessLink.so
  rm $pkgdir$instdir/mplab_ide/mplablibs/modules/lib/libusb-1.0*

  sed -i 's/\/usr\/hitech/\/opt\/hitech/g' $pkgdir/opt/microchip/mplabx/mplab_ide/mplab_ide/modules/com-microchip-mplab-nbide-toolchainhitech.jar

  install -Dm 644 $srcdir/z010_mchp_tools.rules $pkgdir/etc/udev/rules.d/z010_mchp_tools.rules
  install -Dm 644 $srcdir/microchip-mplab.desktop $pkgdir/usr/share/applications/microchip-mplab.desktop
  install -Dm 644 $srcdir/microchip-mplab.png $pkgdir/usr/share/icons/hicolor/48x48/apps/microchip-mplab.png

  mkdir -p $pkgdir/usr/bin
  ln -s $instdir/mplab_ide/bin/mplab_ide $pkgdir/usr/bin/

  install -Dm 644 $srcdir/LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
}
