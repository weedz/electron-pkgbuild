# based on aur electron8-bin: Tom Vincent <http://tlvince.com/contact/>

_projectname=electron
_major=36
_pkgname="${_projectname}${_major}"
pkgname="${_pkgname}"-bin
_pkgver="${_major}.4.0"
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

sha256sums_x86_64=('215623fd1736752f70a273a2ea591a8ce0a63a3c4305866cc30c80505aadc5ca'
  'd2ef32b2bff3fe2594774fca81abda8d617d5f6c0c40529e39900296309e4a3c')

package() {
  install -dm755 "${pkgdir}/usr/lib/${_pkgname}/"
  install -dm755 "${pkgdir}/usr/bin"

  find . -mindepth 1 -maxdepth 1 -type f ! -name "*.zip" ! -name "LICENSE*" -exec cp -r --no-preserve=ownership --preserve=mode -t "${pkgdir}/usr/lib/${_pkgname}/." {} +

  cp -r --no-preserve=ownership --preserve=mode "${srcdir}"/{locales,resources} "${pkgdir}/usr/lib/${_pkgname}"

  chmod u+s "${pkgdir}/usr/lib/${_pkgname}/chrome-sandbox"

  ln -nfs "/usr/lib/${_pkgname}/${_projectname}" "${pkgdir}/usr/bin/${_pkgname}"

  install -Dm644 "${srcdir}/LICENSE"* -t "${pkgdir}/usr/share/licenses/${pkgname}"
}
