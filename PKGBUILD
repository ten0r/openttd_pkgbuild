pkgname=openttd
pkgver=1.8.0
pkgrel=2
pkgdesc='An engine for running Transport Tycoon Deluxe.'
arch=('i686' 'x86_64')
url='http://www.openttd.org'
license=('GPL')
depends=('libpng' 'sdl' 'icu' 'fontconfig' 'lzo' 'hicolor-icon-theme' 'desktop-file-utils' 'xz')
optdepends=('openttd-opengfx: free graphics' 
            'openttd-opensfx: free soundset')
source=("http://binaries.openttd.org/releases/${pkgver}/${pkgname}-${pkgver}-source.tar.xz"
        'polyline_track_tool_v11b_ottd_r27726.diff'
	'fix_6690_icu61.diff')
sha256sums=('c2d32d9d736d27202a020027a3729ae763f5432ae6f424891e57a4095eeb087f'
            '02a23043a72a5a4d0d0bc11c9ad2747994591b0e6feef9725536b33f231992a3'
	    'fb61d7648121f81534c598c6e799f15c49cd9596df0e7e5ced4aa0c32340b412')

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
    --menu-name="OpenTTD"

  make
}

package() {
  cd ${pkgname}-${pkgver} 

  make install
}
