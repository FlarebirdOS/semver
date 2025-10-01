pkgname=semver
pkgver=7.7.2
pkgrel=1
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
sha256sums=(4c9cb3f4a395109aee51926dbb688e31600b2d20277a377ae79f7d65c40af93d)

build() {
    cd node-semver

    npm install
}

package() {
    cd node-semver

    local mod_dir=/usr/lib64/node_modules/${pkgname}

    install -vdm755 ${pkgdir}/{usr/bin,${mod_dir}}

    # lib/ is not currently packaged
    mapfile -t mod_files < <(jq -r '.files[]' package.json | sed '/lib\//d')

    cp -r ${mod_files[@]} LICENSE README.md package.json ${pkgdir}${mod_dir}

    ln -s ${mod_dir}/bin/${pkgname}.js ${pkgdir}/usr/bin/${pkgname}
}
