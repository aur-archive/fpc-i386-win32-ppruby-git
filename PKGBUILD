pkgname=fpc-i386-win32-ppruby-git
pkgver=0.9.2.2.1
pkgrel=1
pkgdesc="Ruby binding units for FreePascal (i386-win32)"
url="https://github.com/shikhalev/ppruby"
license=("GPLv3")
arch=(any)
depends=(fpc-i386-win32-rtl)
makedepends=(ppcross386 git mingw-w64-binutils)
options=(!strip)
source=("${pkgname%-*}::git+https://github.com/shikhalev/ppruby.git")
md5sums=('SKIP')

_unittgt=i386-win32
_fpcver=`fpc -iV`

pkgver () {
	cd "$srcdir/${pkgname%-*}"
	git describe | sed 's|\(.*-.*\)-.*|\1|;s|-|.|'
}

build() {
	cd "${srcdir}/${pkgname%-*}/static"
	ppcross386 -Twin32 ruby18.pp
}

package() {
	cd "${srcdir}/${pkgname%-*}/static"
	find . -name '*.o' -o -name '*.ppu' -o -name '*.rst' -o -name '*.a' |
		xargs -rtl1 -I {} install -Dm644 {} "$pkgdir/usr/lib/fpc/$_fpcver/units/$_unittgt/ppruby/"{}
	find $pkgdir -name '*.o' -o -name '*.a' | xargs -rtl1 i686-w64-mingw32-strip -g
}
