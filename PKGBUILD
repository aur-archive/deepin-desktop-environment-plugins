# Maintainer: Xu Fasheng <fasheng.xu[AT]gmail.com>

### MERGE TO ONE PACKAGE FOR AUR
pkgname='deepin-desktop-environment-plugins'
pkgdesc='Plugins for Linux Deepin desktop environment'

# pkgname=('deepin-desktop-environment-plugins'
         # 'deepin-desktop-environment-plugins-clock'
         # 'deepin-desktop-environment-plugins-weather')
# pkgbase='deepin-desktop-environment-plugins'
pkgver=git20140213151924
pkgrel=1

arch=('any')
url="http://www.linuxdeepin.com/"
license=('GPL2')
makedepends=('coffee-script')

_fileurl=http://packages.linuxdeepin.com/deepin/pool/main/d/deepin-desktop-environment-plugins/deepin-desktop-environment-plugins_0.0.1+git20140213151924~59759d4b18.tar.gz
source=("${_fileurl}")
md5sums=('45dd319db681ac5114afdb0e7ac1470c')

_filename="$(basename "${_fileurl}")"
_filename="${_filename%.tar.gz}"
_innerdir="${_filename/_/-}"

_install_copyright_and_changelog() {
    mkdir -p "${pkgdir}/usr/share/doc/${pkgname}"
    cp -f debian/copyright "${pkgdir}/usr/share/doc/${pkgname}/"
    gzip -c debian/changelog > "${pkgdir}/usr/share/doc/${pkgname}/changelog.gz"
}

prepare() {
    cd "${srcdir}/${_innerdir}"

    # fix python version
    sed -i 's=\(^#! */usr/bin.*\)python=\1python2=' generate_mo update_po
    sed -i 's=python=python2=' weather/makefile
}

package_deepin-desktop-environment-plugins() {
    depends=('deepin-desktop-environment-plugins-clock' 'deepin-desktop-environment-plugins-weather')
    pkgdesc='Meta package for Linux Deepin desktop environment plugins'

    cd "${srcdir}/${_innerdir}"
    _install_copyright_and_changelog
}

package_deepin-desktop-environment-plugins-clock() {
    depends=('deepin-artwork' 'deepin-desktop-environment-common')
    pkgdesc='Linux Deepin desktop environment clock plugin'

    cd "${srcdir}/${_innerdir}"

    (cd clock; make)

    find clock \( -name "*.coffee" -or -name "makefile" \) -delete
    mkdir -p "${pkgdir}"/usr/share/dde/resources/desktop/plugin
    cp -R clock "${pkgdir}"/usr/share/dde/resources/desktop/plugin/

    _install_copyright_and_changelog
}

package_deepin-desktop-environment-plugins-weather() {
    depends=('deepin-artwork' 'deepin-desktop-environment-common')
    pkgdesc='Linux Deepin desktop environment weather plugin'

    cd "${srcdir}/${_innerdir}"

    (cd weather; make)
    find weather \( -name "*.coffee" -or -name "makefile" \) -delete

    mkdir -p "${pkgdir}"/usr/share/dde/resources/desktop/plugin
    cp -R weather "${pkgdir}"/usr/share/dde/resources/desktop/plugin

    _install_copyright_and_changelog
}

### MERGE TO ONE PACKAGE FOR AUR
package() {
    package_deepin-desktop-environment-plugins-clock
    package_deepin-desktop-environment-plugins-weather

    # overwrite variables again, or upload to aur may be failed
    pkgname='deepin-desktop-environment-plugins'
    pkgdesc='Plugins for Linux Deepin desktop environment'
    depends=('deepin-artwork' 'deepin-desktop-environment')
}
