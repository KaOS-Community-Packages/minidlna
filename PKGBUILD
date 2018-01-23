pkgname=minidlna
pkgver=1.2.1
pkgrel=1
pkgdesc="A DLNA/UPnP-AV Media server (aka ReadyDLNA)"
arch=('x86_64')
url="http://sourceforge.net/projects/minidlna/"
license=('GPL')
depends=('libexif' 'libjpeg' 'libid3tag' 'flac' 'libvorbis' 'ffmpeg' 'sqlite')
backup=('etc/minidlna.conf')
install=minidlna.install
source=(http://downloads.sourceforge.net/project/minidlna/minidlna/$pkgver/minidlna-$pkgver.tar.gz
        minidlna.service
        minidlna.tmpfiles)
md5sums=('a968d3d84971322471cabda3669cc0f8'
         'd419b84f0ceda0adae27019a06df5065'
         '26de27b12d6a37c47d9714107d07aac9')

prepare() {
    cd ${srcdir}/${pkgname}-${pkgver}
    sed -i 's|#user=.*|user=nobody|g' minidlna.conf
}

build() {
    cd ${srcdir}/${pkgname}-${pkgver}
    ./configure --prefix=/usr --sbindir=/usr/bin
    make
}

package() {
    cd ${srcdir}/${pkgname}-${pkgver}
    DESTDIR=${pkgdir} make install
    install -Dm644 minidlna.conf ${pkgdir}/etc/minidlna.conf
    install -Dm0644 ${srcdir}/minidlna.tmpfiles ${pkgdir}/usr/lib/tmpfiles.d/minidlna.conf
    install -Dm0644 ${srcdir}/minidlna.service ${pkgdir}/usr/lib/systemd/system/minidlna.service
    install -Dm644 ${srcdir}/${pkgname}-${pkgver}/minidlna.conf.5 ${pkgdir}/usr/share/man/man5/minidlna.conf.5
    install -Dm644 ${srcdir}/${pkgname}-${pkgver}/minidlnad.8 ${pkgdir}/usr/share/man/man8/minidlnad.8
}
