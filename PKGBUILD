pkgname=openttd
pkgver=1.6.0
pkgrel=1
pkgdesc='An engine for running Transport Tycoon Deluxe.'
arch=('i686' 'x86_64')
url='http://www.openttd.org'
license=('GPL')
depends=('libpng' 'sdl' 'icu' 'fontconfig' 'lzo' 'hicolor-icon-theme' 'desktop-file-utils' 'xz')
install=openttd.install
optdepends=('openttd-opengfx: free graphics' 
            'openttd-opensfx: free soundset')
source=("http://binaries.openttd.org/releases/${pkgver}/${pkgname}-${pkgver}-source.tar.xz"
				'polyline_track_tool_v10b_ottd_r27095.diff')
sha256sums=('4c12e6b516ffdee20a03ebad80dad85d137130002d6d3e123a568376fe4b4eb2'
						'74da873263971bcfeca7e57a04abbb4bc59eb3b3be4e15fdb5357fd503807b68')

build() {
  cd ${pkgname}-${pkgver} 
	for _f in "${source[@]}"; do
		[[ "$_f" =~ \.diff$ ]] && {
			msg2 "Applying patch $_f"
			patch -p1 -N --dry-run --silent -i "$srcdir/$_f" 2>/dev/null
			if [ $? -eq 0 ];
			then
				patch -p1 --silent -i "$srcdir/$_f"
				msg2 "Patch $_f applied"
			else
				error "Can't apply patch $_f"
				return 1;
			fi
		}
	done
 ./configure \
    --prefix-dir=/usr \
    --binary-name=${pkgname} \
    --binary-dir=bin \
    --data-dir=share/${pkgname} \
    --install-dir=${pkgdir} \
    --doc-dir=share/doc/${pkgname} \
    --menu-name="OpenTTD" \
    --personal-dir=.${pkgname}    

  make -j6
}

package() {
  cd ${pkgname}-${pkgver} 

  make install
}
