pkgname=udp-obfuscat
pkgver=2.1.0
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
    1fe8be85187d0de95c18684bbe72f6026a14800ab161e882bfb54c8c3b9bbfad
    04e20ed441d2512d054f93fd84a125f2cde493a69b6b82466b709a9f4692db0d
)
backup=(etc/$pkgname/config.toml)

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
