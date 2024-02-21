pkgname=udp-obfuscat
pkgver=2.0.1
pkgrel=1
pkgdesc="UDP proxy with obfuscation"
arch=('x86_64')
url="https://github.com/vehlwn/udp-obfuscat"
license=(ISC)
makedepends=(rust)
source=(
    "$pkgname-$pkgver.tar.gz::https://github.com/vehlwn/$pkgname/archive/$pkgver.tar.gz"
    udp-obfuscat.service
    sysusers.d
)
sha256sums=(
    SKIP
    9ca280084c304114944eda037a8786d2a414fd1a9056a81077cf5968bdbb399c
    04e20ed441d2512d054f93fd84a125f2cde493a69b6b82466b709a9f4692db0d
)

prepare() {
    export RUSTUP_TOOLCHAIN=stable
    cd "$pkgname-$pkgver"
    cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
    export RUSTUP_TOOLCHAIN=stable
    export CARGO_TARGET_DIR=target
    cd "$pkgname-$pkgver"
    cargo build --frozen --release
}

check() {
    cd "$pkgname-$pkgver"
    cargo test --frozen --release --locked
}

package() {
    install -Dm644 $pkgname.service "$pkgdir/usr/lib/systemd/system/$pkgname.service"
    install -Dm644 sysusers.d "$pkgdir/usr/lib/sysusers.d/$pkgname.conf"

    cd "$pkgname-$pkgver"
    install -Dm755 "target/release/$pkgname" "$pkgdir/usr/bin/$pkgname"
    install -Dm644 config-example.toml "$pkgdir/etc/$pkgname/config.toml"
}
