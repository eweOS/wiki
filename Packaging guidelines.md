This guide assumes that you have experience in Arch packaging (if you do not, but have other similar experience,see [Create Packages](https://os-wiki.ewe.moe/A%20quick%20tour%20through%20writing%20PKGBUILD.md)), using common build tools and familiar with basic use of git.

# Create a working environment
See [temporary installation guide](https://os-wiki.ewe.moe/temporary-installation-guide.md). After installation you can browse repositories as normal. We also have `base-devel` like Arch does, but it's a meta package, and is required when building a package.

# Know the basics
eweOS's main changes from Arch Linux, that affects packaging, are clang/llvm and musl.      

## musl
When you see `depends=('glibc')`, you can try change it to `depends=('musl')` firstly. This works in the 95% cases approximately. There are also some problems, usually because musl doesn't have some headers, provide such functions or only made a stub. The common troubles and solutions/workarounds are listed in [musl page](https://os-wiki.ewe.moe/musl).

## clang
Clang and musl is installed by default, and /usr/bin/cc points to clang, so in most cases you don't need to tell build tools you are using it. If you see someone wrote `gcc` in Arch PKGBUILD, simply changing it to `cc` or `clang` is okay. When a package has `depends=('gcc-libs')`, the corresponding depends in llvm is mostly libunwind and libcxx, so changing it to `depends=('llvm-libs')` usually works. See [this page](https://os-wiki.ewe.moe/llvm) for more about clang and llvm.

## mold
In rare cases you may see mold linker reports an error that it can't read some commands from `xxx.ld` or other things. You can specify the default ld (How to specify default ld? Google it) to lld and add `lld` to makedepends. Gold will be introduced soon, but if you use gold, remember to report in the development group.

## Busybox
Busybox provides nearly all of coreutils, half of util-linux and some archive tools and filesystem tools. If you don't know where is the command, use `pacman -F /usr/bin/xxx`. Also use it on Arch Linux, if you've installed one, then you can easily figure out what happens. Busybox doesn't provide libraries, so things like `util-linux-libs` should remain the same. We've renamed `bzip2` to `libbz2`. Don't be afraid to miss any dependencies, since the error will also point out what it exactly needs.

Some busybox commands does not offer some arguments compared to normal ones. Figure out how to use other commands to replace them. Long arguments (such as --compress) are not supported in some commands, replacing them to short ones should work.

## Dinit
Dinit is not a drop-in replacement for systemd, although they are very similar. See [Configuring services](https://github.com/davmac314/dinit#configuring-services) and [Getting Started Guide](https://github.com/davmac314/dinit/blob/master/doc/getting_started.md) for writing and testing dinit service profiles.

## checks
Skip checks sometimes. If checks fails with some unimportant reasons, such as you are running in a chroot container (so remember to run again in a virtual machine to prove it), or other things related to clang and musl about the test itself, you can consider to skip them.

For cmake, append -E [regex] to ctest arguments to ignore these tests. For GNU make & configure or automake, things get harder, but you can find parameters to skip partial test in project Readme, or directly look into Makefile or makefile.am, makefile.in, configure, etc. 

## Others
1. `/usr/share/doc` is dropped till now, so you can safely remove all commands and dependencies (such as doxygen, docbook-xml, docbook-xsl, etc) generating the doc.
2. hashes are ignored, so changing all checksums to SKIP. If b2sums exist, change the name to other sums. We will implement automatically writing hashes in the version bump task (nvchecker very likely) and after build.
3. GPG binary doesn't present. Remove validpgpkeys and asc/sig files in source (they often come with {,sig} or {,asc} ,and SKIP in checksums). This will also be handled in the version bump process.

## Solving unknown issues
1. Remember alpine linux and chimera linux are our best neighbors. Check [their build files](https://os-wiki.ewe.moe/Other%20similar%20distros%20and%20projects.md) if you have anything unknown or uncertain.
2. Search on Google, remember to take keywords musl or clang.
3. Search the project issues.
4. Feel free to ask in the group.

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