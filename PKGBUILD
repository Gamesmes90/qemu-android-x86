# Maintainer: Sam Mulvey <archlinux -at- sammulvey.com>
pkgname=qemu-android-x86
_pkgver="8.1-r2"
pkgver=8.1.r2
pkgrel=1
pkgdesc="Android-x86 environment via QEMU and VirGL"
arch=("x86_64")
url="http://www.android-x86.org/"
license=('Apache' 'GPL2' 'custom:Creative Commons 3.0 Attribution Unported')
depends=('rxvt-unicode' 'zenity' 'qemu' 'hicolor-icon-theme')
makedepends=('inkscape')
install="qemu-android-x86.install"
source=("android-x86-${_pkgver}.${arch}.rpm::https://osdn.net/frs/redir.php?m=auto&f=android-x86%2F69704%2Fandroid-x86-${_pkgver}.${arch}.rpm"
		"https://upload.wikimedia.org/wikipedia/commons/d/d7/Android_robot.svg"
		"qemu-android"
		"config"
		"qemu-android.desktop")
sha256sums=('7280af001b2ad566aad6b1a2e7b5edeea666ee4e5e291d7c623de0fa8a4411ef'
            '8c80b881727efc8831c8ef53806e7c1d0427607e145aae09061c4870b6cd402f'
            'e53911e378a6048d88d4fbaeb870c58f57c44142450527ee99b3c12baa15099a'
            'e9524cdb27c57e6650af763b2231d67ff3e2beb12f52133e7e95eda4f16b0881'
            '8a5ed6a6c1a4dfd1c8af0ff5de48965ec2dc6b50f87e5f990d33c7025f63c8ec')


#PKGEXT=".pkg.tar"

package() {

	mkdir -p $pkgdir/usr/share/android-x86 $pkgdir/usr/bin $pkgdir/usr/share/applications
	install -m0644 $srcdir/android-${_pkgver}/* $pkgdir/usr/share/android-x86
	install -m0644 $srcdir/usr/bin/qemu-android $pkgdir/usr/share/android-x86/original.qemu-android
	install -m0644 $srcdir/config $pkgdir/usr/share/android-x86
	install -m0644 $srcdir/qemu-android.desktop $pkgdir/usr/share/applications
	install -m0755 $srcdir/qemu-android $pkgdir/usr/bin/qemu-android

	iconsizes=(16 32 64 128 256 512)
	for size in "${iconsizes[@]}"; do
		mkdir -p $pkgdir/usr/share/icons/hicolor/${size}x${size}/apps
		inkscape -z -e $pkgdir/usr/share/icons/hicolor/${size}x${size}/apps/qemu-android.png -w $size -h $size $srcdir/Android_robot.svg
	done

}
