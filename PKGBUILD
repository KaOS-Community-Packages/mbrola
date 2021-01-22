pkgname=mbrola
pkgver=3.3
pkgrel=1
pkgdesc='Speech synthesizer based on the concatenation of diphones.'
arch=('x86_64')
url='https://github.com/numediart/MBROLA'
license=('AGPL')
depends=()
makedepends=('make')
source=("https://github.com/numediart/MBROLA/archive/${pkgver}.tar.gz"
        "https://github.com/numediart/MBROLA-voices/blob/master/data/en1/en1?raw=true")
md5sums=('06993903c7b8d3a8d21cc66cd5a28219'
        'eca1e3ae6b8641b6114d1e24a91d6b31')

src_name="MBROLA-${pkgver}"

build() {
    cd ${src_name}
    make
}

package() {
    install -Dm 755 "en1?raw=true" "${pkgdir}/usr/share/mbrola/en1/en1"
    install -Dm 755 "${src_name}/Bin/mbrola" "${pkgdir}/usr/bin/mbrola"
}
