# based on aur electron8-bin: Tom Vincent <http://tlvince.com/contact/>

_projectname=electron
_major=34
_pkgname="${_projectname}${_major}"
pkgname="${_pkgname}"-bin
_pkgver="${_major}.1.1"
pkgver="${_pkgver/-/.}"
pkgrel=1
pkgdesc="Build cross platform desktop apps with web technologies - binary version ${_major}"
arch=('x86_64')
url=https://electronjs.org/
license=('MIT' 'LicenseRef-custom')
provides=("${_pkgname}=${pkgver}" "${_projectname}=${pkgver}")
conflicts=("${_pkgname}")
depends=(c-ares
  alsa-lib
  gtk3
  libevent
  libffi
  nss)
optdepends=('wayland'
  'pipewire: WebRTC desktop sharing under Wayland'
  'kde-cli-tools: file deletion support (kioclient5)'
  'libappindicator-gtk3: StatusNotifierItem support'
  'qt5-base: enable Qt5 with --enable-features=AllowQt'
  'trash-cli: file deletion support (trash-put)'
  'xdg-utils: open URLs with desktop’s default (xdg-email, xdg-open)')
_releaseurl="https://github.com/${_projectname}/${_projectname}/releases/download/v${_pkgver}"
source_x86_64=(
  "${pkgname}-chromedriver-${pkgver}-x86_64.zip::${_releaseurl}/chromedriver-v${_pkgver}-linux-x64.zip"
  "${pkgname}-${pkgver}-x86_64.zip::${_releaseurl}/${_projectname}-v${_pkgver}-linux-x64.zip"
)

sha256sums_x86_64=('62734cb681a6da3c73b20504f49c7759c9dbb1c923e250d67c11888426e3cad0'
  '9fbca20baea84800f7f50a9b245302dddbfab3425dd762c482d79e867a5a6dbe')

package() {
  install -dm755 "${pkgdir}/usr/lib/${_pkgname}/"
  install -dm755 "${pkgdir}/usr/bin"

  find . -mindepth 1 -maxdepth 1 -type f ! -name "*.zip" ! -name "LICENSE*" -exec cp -r --no-preserve=ownership --preserve=mode -t "${pkgdir}/usr/lib/${_pkgname}/." {} +

  cp -r --no-preserve=ownership --preserve=mode "${srcdir}"/{locales,resources} "${pkgdir}/usr/lib/${_pkgname}"

  chmod u+s "${pkgdir}/usr/lib/${_pkgname}/chrome-sandbox"

  ln -nfs "/usr/lib/${_pkgname}/${_projectname}" "${pkgdir}/usr/bin/${_pkgname}"

  install -Dm644 "${srcdir}/LICENSE"* -t "${pkgdir}/usr/share/licenses/${pkgname}"
}
