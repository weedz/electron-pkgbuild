# based on aur electron8-bin: Tom Vincent <http://tlvince.com/contact/>

_projectname=electron
_major=32
_pkgname="${_projectname}${_major}"
pkgname="${_pkgname}"-bin
_pkgver="${_major}.2.1"
pkgver="${_pkgver/-/.}"
pkgrel=1
pkgdesc="Build cross platform desktop apps with web technologies - binary version ${_major}"
arch=('x86_64' 'aarch64')
url=https://electronjs.org/
license=('MIT')
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

sha256sums_x86_64=('2329d1307729c714bef71d9f8250ed510b5a1ae07beefddee2371af70f712297'
  '4fc58e6e79e5b5793ec9b5d35c8926fcad5352b6a1b21b3edf42343487c90185')

package() {
  install -dm755 "${pkgdir}/usr/lib/${_pkgname}/"
  find . -mindepth 1 -maxdepth 1 -type f ! -name "*.zip" ! -name "LICENSE*" -exec cp -r --no-preserve=ownership --preserve=mode -t "${pkgdir}/usr/lib/${_pkgname}/." {} +

  for _folder in 'locales' 'resources'; do
    cp -r --no-preserve=ownership --preserve=mode "${_folder}/" "${pkgdir}/usr/lib/${_pkgname}/${_folder}/"
  done

  chmod u+s "${pkgdir}/usr/lib/${_pkgname}/chrome-sandbox"

  install -dm755 "${pkgdir}/usr/bin"
  ln -nfs "/usr/lib/${_pkgname}/${_projectname}" "${pkgdir}/usr/bin/${_pkgname}"

  for _license in 'LICENSE' 'LICENSES.chromium.html'; do
    install -Dm644 "${_license}" "${pkgdir}/usr/share/licenses/${pkgname}/${_license}"
  done
}
