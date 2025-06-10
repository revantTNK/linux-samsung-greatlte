# Reference: <https://postmarketos.org/vendorkernel>
# Kernel config based on: arch/arm64/configs/(CHANGEME!)

pkgname=linux-samsung-greatlte
pkgver=4.4.302
pkgrel=0
pkgdesc="Samsung Galaxy Note 8 Exynos kernel fork"
arch="aarch64"
_carch="arm64"
_flavor="samsung-greatlte"
url="https://kernel.org"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native"
makedepends="
	bash
	bc
	bison
	devicepkg-dev
	findutils
	flex
	openssl-dev
	perl
"

# Source
_repository="android_kernel_samsung_universal8895"
_commit="76ccdeff9dac383738bb47d15db9b4ca2556376f"
_config="config-$_flavor.$arch"
source="
	$pkgname-$_commit.tar.gz::https://github.com/8890q/$_repository/archive/$_commit.tar.gz
	$_config
	fix-check-lxdialog.patch
"
builddir="$srcdir/$_repository-$_commit"
_outdir="out"

prepare() {
	default_prepare
	. downstreamkernel_prepare
}

build() {
	unset LDFLAGS
	make O="$_outdir" ARCH="$_carch" CC="${CC:-gcc}" \
		KBUILD_BUILD_VERSION="$((pkgrel + 1 ))-postmarketOS"
}

package() {
	downstreamkernel_package "$builddir" "$pkgdir" "$_carch" \
		"$_flavor" "$_outdir"
}

sha512sums="
5dbdc7c7d6451a236379773e2f0a4046582f3652a0113285e0baca7501cd050104a2c60b810367041a1a94143d9b13e37690a04ff1c8d51e0ca24e2e7540cf88  linux-samsung-greatlte-76ccdeff9dac383738bb47d15db9b4ca2556376f.tar.gz
552a9d1f0a5d332e444df555264732c0c75f5218dc4bd066c40275412107b1cb416c8d0be0a703ceac6e2674085fb1edf080910add034bd536b0c8d3bfd669a7  config-samsung-greatlte.aarch64
182be3c596b9cc267ac108d7cf03fc8c328ccc6b36770800e4dcedea8d1bb65e3f5eacf590c2948f58b1418cc60a1670ba77dde8c259e428d158c31b6e1dbaf5  fix-check-lxdialog.patch
"
