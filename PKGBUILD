_pkgname=bamboo
pkgname=atlassian-${_pkgname}
pkgver=6.2.1
pkgrel=1
pkgdesc="Bamboo Server"
url="https://www.atlassian.com/software/${_pkgname}"
license=("custom")
arch=("i686" "x86_64")
depends=("java-runtime=8"
        "git>=1.8.0"
        "perl>=5.8.8")
optdepends=("haveged: Entropy for the ssh plugin" )
backup=("etc/systemd/system/${_pkgname}.service.d/local.conf"
        "etc/${_pkgname}/server.xml")
install="$pkgname.install"
options=(!strip)
source=("https://www.atlassian.com/software/${_pkgname}/downloads/binary/${pkgname}-${pkgver}.tar.gz"
        "${_pkgname}.service"
        "${_pkgname}.tmpfiles"
        "${_pkgname}.sysusers"
        "local.conf")

package() {
    install -dm750 "$pkgdir/var/lib/${_pkgname}"
    install -dm750 "$pkgdir/var/lib/${_pkgname}/tmp"
    install -dm755 "$pkgdir/opt/$pkgname"
    install -dm755 "$pkgdir/usr/share/licenses/$pkgname"
    cp -r "$srcdir/atlassian-${_pkgname}-$pkgver/licenses/"* "$pkgdir/usr/share/licenses/$pkgname"
    cp -r "$srcdir/atlassian-${_pkgname}-$pkgver/"* "$pkgdir/opt/$pkgname"
    install -Dm755 "$pkgdir/opt/$pkgname/conf/server.xml" "$pkgdir/etc/${_pkgname}/server.xml"
    rm "$pkgdir/opt/$pkgname/conf/server.xml"
    ln -sf "/etc/${_pkgname}/server.xml" "$pkgdir/opt/$pkgname/conf/server.xml"
    # remove unneeded Windows files
    find "$pkgdir/opt/$pkgname/bin" -name "*.bat" -type f -exec rm "{}" \;
    find "$pkgdir/opt/$pkgname/bin" -name "*.exe" -type f -exec rm "{}" \;


    # setup systemd service
    install -Dm644 "$srcdir/${_pkgname}.service" "$pkgdir/usr/lib/systemd/system/${_pkgname}.service"
    install -Dm644 "$srcdir/local.conf" "$pkgdir/etc/systemd/system/${_pkgname}.service.d/local.conf"
    install -Dm644 "$srcdir/${_pkgname}.tmpfiles" "$pkgdir/usr/lib/tmpfiles.d/${_pkgname}.conf"
    install -Dm644 "$srcdir/${_pkgname}.sysusers" "$pkgdir/usr/lib/sysusers.d/${_pkgname}.conf"
}

sha256sums=('f21102bd2e324bb04e4dc727e586f640142d42ff98d474227fb2aa6ea8aa8212'
            '26d456375bbdac2dfee5a1d19f573adf82e4dc4d51417d9d14a963391338f3e9'
            'f9822491daf68fdc1ad30aa3b8bd1a5efb8f599f45c7915379079e42479f2365'
            '8612657716df1be0a61fe77c88648d96d08b5c98c0a6b9fbd76cb40f1c0bba95'
            '6af60498198e1db22999bf65a17105c9652eb8758b531096bc69d534f17ee742')
