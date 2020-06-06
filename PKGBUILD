# Maintainer: Ross Clark <archiv8@artisteducator.com>
# Contributor: Ross Clark <archiv8@artisteducator.com>


#_langname=""
_relname="synfig"
_partname="core"
#_cvsname=""


# pkgbase=
pkgname="${_relname}-${_partname}"
pkgver=1.3.14
pkgrel=1
# epoch=
pkgdesc="Open-source 2D Animation Software. Core package providing a GUI to Synfig core"
arch=("x86_64")
url="https://www.synfig.org/"
license=("GPL2")
# groups=()
depends=("bash")
# optdepends=()
makedepends=("cmake" "git")
# checkdepends=()
# provides=()
conflicts=("etl")
replaces=("etl")
# backup=()
# options=()
# install=
changelog="CHANGELOG.md"
source=(
"${_relname}-v${pkgver}.tar.gz::https://github.com/${_relname}/${_relname}/archive/v${pkgver}.tar.gz"
"CC-BY-SA-V4.md"
"CHANGELOG.md"
"CODE-OF-CONDUCT.md"
"CONTRIBUTE.md"
"DEPENDENCIES.md"
"DEVELOPER-CERTIFICATE-OF-ORIGIN.md"
"INSTALL.md"
"ISSUES.md"
"LICENSE.md"
"MIT.md"
"OPTIONS.md"
"README.md"
)
# noextract=()
# validpgpkeys=()
sha256sums=('f2872c0c1cea9c60f4ddcb36439963b33b3d5cba790d7a800c2923fd0b4ef1cb'
            'b92d2feed74cb73994f5b76ec511abafa12ed5b681db844191c4e32939948aaf'
            'a6bbded8c6e93eab74d8e738b24620f2ac968b9774729fe5ee12f032b706e913'
            '8177592fe733e9183ee400ed6c396793f0e188844f2dd775caceb0fde3503443'
            'e0d506d4f50dfdc61722487ede4a7aaadabb608f3df2c55ef97f99bb388a6431'
            '5f0f69583e8c9415b625fad037a6f6e96859ca65a26fd2c4cd7880aa78f7c1c1'
            'f70a73f588fbcf85ee4ae8b002d8a0a1a0efcfb73043a4eeb394b851547fbd53'
            'c760b51b1dd883c78a5fb9df32698fbe44b37fe165d9a6661da262d3af938d36'
            '25ddb2d1c3726b9adb624cf24f3a5e64a6e8d7392ebaf9f4d1e49c62bccf17dc'
            'c0d587af5ba492d3bc18b71b823c9a7b8cf721a004c31fad5efaba28b10461b1'
            'a92793ddaca37fe7da780d10613604b52969368f5fbec3c67eb20edb988b4f49'
            'f28a7d18f2c7c0083f912fba147b572533856557e767ad7cbab75bb18d2880f6'
            '2d2e06d754f728afa14a15ecc6870cef21eef19343102728bcae55ef492a8046')

prepare () {

  # Change to the Synfig ETL directory
  cd "${srcdir}/${_relname}-${pkgver}/synfig-core"

  # Bootstrap as not installing via provided scripts.
  ./bootstrap.sh

  # Run configure script
  ./configure \
  --prefix=/usr \
  --sysconfdir=/etc/synfig
}

build() {

  # Change to the Synfig ETL directory
  cd "${srcdir}/${_relname}-${pkgver}/ETL"

  # Run make
  make
}

# check() {}

package() {

  # Change to the Synfig ETL directory
  cd "${srcdir}/${_relname}-${pkgver}/ETL"

  # Install the Synfig ETL library
  make DESTDIR="${pkgdir}" install

  # Install the Synfig ETL documentation
  install -Dm 644 "${srcdir}/${_relname}-${pkgver}/ETL/NEWS" "${pkgdir}/usr/share/doc/${pkgname}/NEWS"
  install -Dm 644 "${srcdir}/${_relname}-${pkgver}/ETL/NEWS" "${pkgdir}/usr/share/doc/${pkgname}/README"

  # Install the Synfig ETL license
  install -Dm 644 "${srcdir}/${_relname}-${pkgver}/ETL/config/pkg-support/devel-resources/License.rtf" "${pkgdir}/usr/share/licenses/${pkgname}/License.rtf"

  # Create the Archiv8 Documentation folder
  install -dvm 755 "${pkgdir}/usr/share/doc/${pkgname}/packaging/"

  # Install the Archiv8 Documentation
  install -Dm 644 "${srcdir}/CC-BY-SA-V4.md" "${pkgdir}/usr/share/doc/${pkgname}/packaging/CC-BY-SA-V4.md"
  install -Dm 644 "${srcdir}/CHANGELOG.md" "${pkgdir}/usr/share/doc/${pkgname}/packaging/CHANGELOG.md"
  install -Dm 644 "${srcdir}/CODE-OF-CONDUCT.md" "${pkgdir}/usr/share/doc/${pkgname}/packaging/CODE-OF-CONDUCT.md"
  install -Dm 644 "${srcdir}/CONTRIBUTE.md" "${pkgdir}/usr/share/doc/${pkgname}/packaging/CONTRIBUTE.md"
  install -Dm 644 "${srcdir}/DEPENDENCIES.md" "${pkgdir}/usr/share/doc/${pkgname}/packaging/DEPENDENCIES.md"
  install -Dm 644 "${srcdir}/DEVELOPER-CERTIFICATE-OF-ORIGIN.md" "${pkgdir}/usr/share/doc/${pkgname}/packaging/DEVELOPER-CERTIFICATE-OF-ORIGIN.md"
  install -Dm 644 "${srcdir}/INSTALL.md" "${pkgdir}/usr/share/doc/${pkgname}/packaging/INSTALL.md"
  install -Dm 644 "${srcdir}/ISSUES.md" "${pkgdir}/usr/share/doc/${pkgname}/packaging/ISSUES.md"
  install -Dm 644 "${srcdir}/LICENSE.md" "${pkgdir}/usr/share/doc/${pkgname}/packaging/LICENSE.md"
  install -Dm 644 "${srcdir}/MIT.md" "${pkgdir}/usr/share/doc/${pkgname}/packaging/MIT.md"
  install -Dm 644 "${srcdir}/OPTIONS.md" "${pkgdir}/usr/share/doc/${pkgname}/packaging/OPTIONS.md"
  install -Dm 644 "${srcdir}/README.md" "${pkgdir}/usr/share/doc/${pkgname}/packaging/README.md"
}
