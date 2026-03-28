# Maintainer: Martin Chang <marty188586 at gmail dot com>
pkgname=restool
pkgver=6.6.52
_pkgver=lf-6.6.52-2.2.0
pkgrel=0
pkgdesc="An user space application providing the ability to dynamically create and manage NXP DPAA2 containers and objects from Linux."
arch=('aarch64' 'armv7h' 'armv6h')
url="https://github.com/nxp-qoriq/restool"
license=('GPL')
depends=()
makedepends=(git make gcc)
provides=(restool)
source=("git+https://github.com/nxp-qoriq/restool.git#tag=$_pkgver")
sha1sums=('SKIP')

build() {
  cd "$srcdir/$pkgname"

  # Provide a dummy pandoc so make install can skip man page generation
  mkdir -p "$srcdir/bin"
  cat > "$srcdir/bin/pandoc" << 'EOF'
#!/bin/sh
out=""
next=0
for arg; do
  if [ "$next" = 1 ]; then out="$arg"; next=0
  elif [ "$arg" = "-o" ]; then next=1; fi
done
[ -n "$out" ] && touch "$out"
EOF
  chmod +x "$srcdir/bin/pandoc"
  export PATH="$srcdir/bin:$PATH"

  make
}

package() {
  cd "$srcdir/$pkgname"
  export PATH="$srcdir/bin:$PATH"

  make DESTDIR="$pkgdir/" prefix="/usr/" install
}
