# based on aur electron8-bin: Tom Vincent <http://tlvince.com/contact/>

_projectname=electron
_major=36
_pkgname="${_projectname}${_major}"
pkgname="${_pkgname}"-bin
_pkgver="${_major}.2.1"
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

sha256sums_x86_64=('be491846efc96dec5cfc19f064f0586008c2cb8a664ef556be50338e7107ba7a'
  '6ede19133495925c6fd39dcc161d255372a1cd0d2dc8c131929233584498be35')

package() {
  install -dm755 "${pkgdir}/usr/lib/${_pkgname}/"
  install -dm755 "${pkgdir}/usr/bin"

  find . -mindepth 1 -maxdepth 1 -type f ! -name "*.zip" ! -name "LICENSE*" -exec cp -r --no-preserve=ownership --preserve=mode -t "${pkgdir}/usr/lib/${_pkgname}/." {} +

  cp -r --no-preserve=ownership --preserve=mode "${srcdir}"/{locales,resources} "${pkgdir}/usr/lib/${_pkgname}"

  chmod u+s "${pkgdir}/usr/lib/${_pkgname}/chrome-sandbox"

  ln -nfs "/usr/lib/${_pkgname}/${_projectname}" "${pkgdir}/usr/bin/${_pkgname}"

  install -Dm644 "${srcdir}/LICENSE"* -t "${pkgdir}/usr/share/licenses/${pkgname}"
}
