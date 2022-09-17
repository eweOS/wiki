This guide assumes that you have experience in Arch packaging, using common build tools and familiar with basic use of git.

# Create a working environment
See [temporary installation guide](https://os-wiki.ewe.moe/temporary-installation-guide.md). After installation you can browse repositories as normal. We also have `base-devel` like Arch does, but it's a meta package, and is required when building a package.

# Get permissions
Contact @yukarichiba in our [matrix space](https://matrix.to/#/#os:ewe.moe), and she will invite you to our GitHub organization.

# Choose repo to place package
This is the logic of choosing repos (match in order):        
1. `desktop`. The package contains graphical programs, or renders animations, or plays sound, etc. Everything that is usually available only on a system that covers a desktop, should be placed here.
2. `minimal`. The package is in minimal liveiso. Please discuss in group if you'd like to add a package here.
3. `develop`. The package contains building tools, which means that it only needed for programming and building programs most of time(If you search it on Arch Official Repository, you may see a lot of (make) in "Required By".)
4. `network`. The package is related to managing network connections, handle download, is related to cyber security, etc. Libraries also included.
5. `kernek`. Only Linux kernels and kernel headers.
6. `boot`. The package contains bootloaders, EFI managers, firmware managers, initramfs creators, etc. Everything related to the boot process before init.
7. `misclibs`. The package only contains libraries and headers, or it has some binary executables but they are only required in a very limited conditions, and are very unlikely to be used by normal users.
8. `misc`. The package does not belong to the above categories.

# Submit the package
_Note: A script is available [here](https://github.com/eweOS/useful-scripts/blob/main/pkg-submit/pkg-submit.sh), but may not be stable._         
Assuming that you've successfully created a package, and got permissons.        
Firstly, clone the repo `pkgs`.
```
git clone git@github.com:eweOS/pkgs.git
```
Then create an orphan branch and place your build files (including PKGBUILD) in it(Remember also remove unnecessary files except .git). The branch name should be repo/package, for example, minimal/zlib-ng.
```
git checkout --orphan desktop/your-package
```
After doing all these, you can submit directly.
```
git stage .
git commit -m "xxx"
git push --set-upstream origin desktop/your-package
```
A corresponding package will be created automatically on os-build.ewe.moe, and start building.