# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Maintainer: Bennett Petzold <dansecob.aur gmail com>

BUILDENV+=(!check)

pkgname=qsv
pkgver=0.131.1
pkgrel=1
pkgdesc='CSV data-wrangling toolkit (fork of xsv)'
arch=(x86_64)
url="https://github.com/jqnatividad/$pkgname"
license=(MIT Unlicense)
depends=(python
         python-xlsxwriter)
makedepends=(cargo
             clang
             luau)
_archive="$pkgname-$pkgver"
options=(!lto)
source=("$url/archive/$pkgver/$_archive.tar.gz")
sha256sums=('9038f09a0e1523bcf3a993bd95a36f8dd1c640e7ffbbe9404e018d41a7d82b66')

prepare() {
	cd "$_archive"
	cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
	sed -i -e '/^lto/s/true/false/' Cargo.toml
}

_srcenv() {
	cd "$_archive"
	export RUSTUP_TOOLCHAIN=stable
	export CARGO_TARGET_DIR=target
}

build() {
	_srcenv
	env \
		CARGO_PROFILE_RELEASE_LTO=true \
		CARGO_PROFILE_RELEASE_CODEGEN_UNITS=1 \
		CARGO_PROFILE_RELEASE_DEBUG=2 \
	cargo build --frozen --release --features distrib_features
}

check() {
	_srcenv
	cargo test --frozen --features distrib_features
}

package() {
	cd "$_archive"
	install -Dm0755 -t "$pkgdir/usr/bin/" "target/release/$pkgname"
	install -Dm644 -t "$pkgdir/usr/share/elvish/lib/" contrib/completions/examples/qsv.elv
	install -Dm644 -t "$pkgdir/usr/share/fish/vendor_completions.d/" contrib/completions/examples/qsv.fish
	install -Dm644 contrib/completions/examples/qsv.bash "$pkgdir/usr/share/bash-completion/completions/qsv"
	install -Dm644 contrib/completions/examples/qsv.zsh "$pkgdir/usr/share/zsh/site-functions/_qsv"
}
