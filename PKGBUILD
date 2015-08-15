# Maintainer: Jim Pryor <profjim@jimpryor.net>
# Warning: The chicken-* egg PKGBUILDS in AUR are auto-generated.
#          Please report errors you notice so that I can tweak the generation script.

pkgname=chicken-wmiirc
pkgver=0.4
pkgrel=4
pkgdesc="Chicken Scheme Egg: A library for writing wmii configuration scripts"
arch=('i686' 'x86_64')
url="http://chicken.wiki.br/eggref/4/wmiirc"
license=('BSD')
depends=('chicken>=4.5.0' 'chicken-9p' 'chicken-unix-sockets' )
options=(docs !libtool !emptydirs)
install="chicken.install"
source=("$pkgname-$pkgver.chunked::http://chicken.kitten-technologies.co.uk/henrietta.cgi?name=wmiirc&version=$pkgver"
		"$pkgname-$pkgver.html::http://chicken.wiki.br/eggref/4/wmiirc.html")
md5sums=('c39634fe7491d056cce1e9c1341f074d' '69d3527f744951c1d6657d2c0d8ee9d2')

build() {
	# unchunk the blob that was downloaded from henrietta
	cd "$srcdir"
	mkdir -p "wmiirc-$pkgver"
	cat "$pkgname-$pkgver.chunked" | while :; do
		while read -r bar ver endbar fname len; do
			[[ -n "$ver" ]] && break
		done
		[[ "$endbar" = "|#" ]] || fname="$ver" len="$endbar"
		[[ -z "$fname" ]] && break
		fname="${fname:1:${#fname}-2}" # delete quotes around fname
		if [[ "${fname: -1}" == / ]]; then
			mkdir -p "wmiirc-$pkgver/$fname"
		elif [[ "$len" -eq 0 ]]; then
			touch "wmiirc-$pkgver/$fname"
		else
			dd iflag=fullblock of="wmiirc-$pkgver/$fname" ibs="$len" count=1 2>/dev/null
		fi
	done
	

	cd "$srcdir/wmiirc-$pkgver"
	cp ../$pkgname-$pkgver.html wmiirc.html
	
	
	mkdir -p "$pkgdir/usr/lib/chicken/5" "$pkgdir/usr/share/chicken/wmiirc"
		
	chicken-install -p "$pkgdir/usr"
	
		install -Dm644 "wmiirc.html" "$pkgdir/usr/share/doc/$pkgname/wmiirc.html"
}
