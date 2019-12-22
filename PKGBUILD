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
source=("git+https://github.com/tpoechtrager/$_reponame.git#commit=$_commit")
sha256sums=('SKIP')
noextract=("$_sdkname.tar.xz")
options=('!strip')

build() {
  cd "$srcdir/$_reponame/usage_examples/ios_toolchain"

  msg2 'Build ioscross'
  ./build.sh "$startdir/$_sdkname.sdk.tar.xz" arm64
}

package() {
  cd "$srcdir/$_reponame/usage_examples/ios_toolchain"

  mkdir -p "$pkgdir/opt"
  cp -r target "$pkgdir/opt/ioscross"
}
