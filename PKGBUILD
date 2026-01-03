pkgname=semver
pkgver=7.7.3
pkgrel=2
pkgdesc="The semantic version parser used by npm"
arch=('x86_64')
url="https://github.com/npm/node-semver"
license=('ISC')
depends=('nodejs')
makedepends=(
    'git'
    'jq'
    'npm'
)
source=(git+ssh://git@github.com/npm/node-semver.git#tag=v${pkgver})
sha256sums=(744a5c92eb4da06f999bfaee77fe01424f5cd9140c830deb83af6af0ef00f368)

prepare() {
    cd node-semver

    npm install
}

package() {
    cd node-semver

    local mod_dir=/usr/lib/node_modules/${pkgname}

    install -vdm755 ${pkgdir}/{usr/{bin,share/doc/${pkgname}},${mod_dir}}

    ln -s ${mod_dir}/bin/${pkgname}.js ${pkgdir}/usr/bin/${pkgname}
    ln -s ${mod_dir}/README.md ${pkgdir}/usr/share/doc/${pkgname}

    # lib/ is not currently packaged
    mapfile -t mod_files < <(jq -r '.files[]' package.json | sed '/lib\//d')
    cp -r ${mod_files[@]} LICENSE README.md package.json ${pkgdir}/${mod_dir}
}
