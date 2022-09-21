PKGBUILD is actually a type of bash script, which defines basic infomation of the package, and how to build, test and composing build artifacts into packages. You need to be familiar with the common syntax of bash first.

See [PKGBUILD - Arch Wiki](https://wiki.archlinux.org/title/PKGBUILD#Version) for a detailed instructions for writing PKGBUILD.

Let's start with a normal PKGBUILD `jq` first.
```
# Maintainer: Aleksana QwQ <me@aleksana.moe>
# Contributor: Evgeniy Alekseev <arcanis at archlinux dot org>
# Contributor: Alex Chamberlain <alex at alexchamberlain dot co dot uk>
# Contributor: Kars Wang <jaklsy at gmail dot com>

pkgname=jq
pkgver=1.6
pkgrel=4
pkgdesc='Command-line JSON processor'
arch=('x86_64')
url='https://stedolan.github.io/jq/'
license=('MIT')
depends=('musl' 'oniguruma')
makedepends=('bison' 'flex' 'python')
source=("https://github.com/stedolan/jq/releases/download/${pkgname}-${pkgver}/${pkgname}-${pkgver}.tar.gz")
sha512sums=('SKIP')

build() {
    cd "${pkgname}-${pkgver}"
    ./configure --prefix=/usr
    make
}

check() {
    cd "${pkgname}-${pkgver}"
    make check
}

package() {
    cd "${pkgname}-${pkgver}"
    make DESTDIR="${pkgdir}" prefix=/usr install
    install -Dm644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
}
```

# Basic info
At the head of this PKGBUILD includes several lines containing maintainers' names and email addresses. 
- `# Maintainer` means the person will handle issues and upgrades. 
- `# Contributor` means the person contributed to (directly interacted with the directory where this PKGBUILD is stored) the PKGBUILD and releavant build files, such as patches. It usually means this person was the maintainer of this PKGBUILD, but does not participate in this project, or has't been active for a relatively long time, or has given up maintainence of this package. Contributors are not expected to handle issues and upgrades.

If you are adopting PKGBUILDs from Arch Linux or AUR, It is advised to reserve these information, but change `Maintainer` to `Contributor` to avoid our build bot or users accidentally sending spam mails to them.

Also, you may see many forms of writing email address in Arch official repo. But we need to extract the information for the detail page and build bot（in near future), so please only write `<foo@bar.xxx>` as maintainers' email addresses. Again, the contributors' don't have to change.

# writing depends
Note that there are two meta packages, `base` and `base-devel`. The dependencies of `base` are not required in `depends` and those of `base-devel` are not required in `makedepends`. Do not include dependencies in `depends` again in `makedepends`, since when making packages both are installed. 

`optdepends` are only noticed when the user install packages. Please write `'package: for doing something'` to make their use cases clear.

# writing sources
Replace package version in source link with `${pkgver}` to work with automatic updates.

# writing functions
Supposing that the source contains a `xxx.tar.gz` (regular formats of archive files are automatically unzipped), and it builds a package `foo`, the build directory looks like this
```
├── PKGBUILD
├── xxx.tar.gz
├── pkg
│   └── foo
│       └──...
└── src
    ├── xxx.tar.gz -> ../xxx.tar.gz
    └── yyy (automatically unzipped folder of xxx.tar.gz)
```
The `$srcdir` stands for absolute directory of src and `$pkgdir` stands for that of foo.

Every function, `package` included, starts on directory $srcdir.