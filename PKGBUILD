# Maintainer: mikezackles <mikezackles@gmail.com>

# Adjust this to point to your Xcode download. This PKGBUILD assumes it is a .xip that 
_sdkname=iPhoneOS13.2

_reponame=cctools-port
pkgname=ioscross
_revccount=200
_commit=8239a52
pkgver=$_revccount.$_commit
pkgrel=1
pkgdesc='iOS cross toolchain'
arch=('x86_64')
url='https://github.com/tpoechtrager/$_reponame'
license=('MIT')
depends=()
makedepends=('git' 'libxml2' 'clang>=3.2' 'cmake' 'python' 'libc++')
provides=("$pkgname")
conflicts=("$pkgname")
source=(
  "git+https://github.com/tpoechtrager/$_reponame.git#commit=$_commit"
  "$_sdkname.sdk.tar.xz"
  'meson.cross'
)
sha256sums=(
  'SKIP'
  '1d2a6d863c7956b5c43ec4f294f880b7fecd59d4d51b16d0660cc32422e2057c'
  'b3938d984e05a4e88b21c1793ba60e98d4fc7c46493b04411bd7f5d18ea1bff3'
)
noextract=("$_sdkname.tar.xz")
options=('!strip')

build() {
  cd "$srcdir/$_reponame/usage_examples/ios_toolchain"

  msg2 'Build ioscross'
  #./build.sh "$startdir/$_sdkname.sdk.tar.xz" arm64
  ./build.sh "$srcdir/$_sdkname.sdk.tar.xz" arm64
}

package() {
  mkdir -p "$pkgdir/opt"
  mkdir -p "$pkgdir/usr/bin"
  mkdir -p "$pkgdir/usr/local/share/meson/cross"
  cp -r "$srcdir/$_reponame/usage_examples/ios_toolchain/target" "$pkgdir/opt/ioscross"

  # ldid needs to be visible on PATH
  ln -s /opt/ioscross/bin/ldid "$pkgdir/usr/bin/ldid"

  # Install meson cross file
  install -Dm644 "$srcdir/meson.cross" "$pkgdir/usr/local/share/meson/cross/ios"
}
