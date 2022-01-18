# Package.yml

All packages consist of a single build file, which provides all of the required metadata for the package manager, plus the build steps involved to produce a package. This follows the YAML specification.

## Format

All `package.yml` files **must** be valid YAML.

As can be seen in the example below, the file is organised into a key-&gt;value hierarchy. Some values may be required to be in a list format, whereas most are simple strings. The build step sections are all considered optional, however if you do not 
perform *any* steps, then no package is generated. Each of these keys contains content that will be placed within a script and executed within a controlled environment to perform the package build. To all intents and purposes, they are bash scripts 
with a predefined environment.

An example file follows:

``` yaml
name       : nano
version    : 2.9.5
release    : 96
source     :
    - https://www.nano-editor.org/dist/v2.9/nano-2.9.5.tar.xz : 7b8d181cb57f42fa86a380bb9ad46abab859b60383607f731b65a9077f4b4e19
license    : GPL-3.0-or-later
summary    : Small, friendly text editor inspired by Pico
component  : system.devel
description: |
    GNU nano is an easy-to-use text editor originally designed as a replacement for Pico, the ncurses-based editor from the non-free mailer package Pine (itself now available under the Apache License as Alpine).
setup      : |
    %patch -p1 < $pkgfiles/0001-Use-a-stateless-configuration.patch
    %reconfigure --enable-utf8 --docdir=/usr/share/doc/nano
build      : |
    %make
install    : |
    %make_install
    install -D -m 00644 $pkgfiles/nanorc $installdir/usr/share/defaults/nano/nanorc
    install -D -m 00644 $pkgfiles/git.nanorc $installdir/usr/share/nano/git.nanorc
    # https://github.com/scopatz/nanorc
    for rcFile in $pkgfiles/nanorc-extras/*.nanorc; do
        install -m 00644 $rcFile $installdir/usr/share/nano
    done
```

## Keys

Not all fields in `package.yml` are mandatory, but a small selection are. They are listed below. Note that `string(s)` indicates that it is possible to use a `list` of strings, or one single `string`

`dict` refers to a `key : value` split in YAML, and `dict(s)` refers to a list of `dict`s

### Mandatory Keys

Key Name | Type | Description
---- | ---- | ----
**name** | `string` | The name of the package. This is also used as the base of all sub-package names. Unless unavoidable, this should match the upstream name
**version** | `string` | The version of the currently packaged software. This is taken from the tarball in most cases.
**release** | `integer` | Specifies the current release number. Updates in the package number are based on this `release` number, *not* the `version` number. As such, to release an update to users, this number must be incremented by one.
**license** | `string(s)` | Valid upstream license(s). Try to ensure these use [SPDX identifiers](https://spdx.org/licenses/).
**source** | `dict(s)` | Upstream source location (i.e. tarball), with the valid `sha256sum` as a value
**component** | `string` | Component / group of packages this package belongs to. Check available components via `eopkg lc`
**summary** | `string` | Brief package summary, or display name
**description** | `string` | More extensive description of the software, usually taken from the vendor website

### Optional, supported keys

Key Name | Type | Description
---- | ---- | ----
**clang** | `bool` | Set to `no` if this package cannot be built with Clang
**extract** | `bool` | Set to `no` to disable automatic source extraction.
**autodep** | `bool` | Set to `no` to disable automatic binary dependency resolution at build time
**emul32** | `bool` | Set to `yes` to enable an `-m32` build (32-bit libs)
**libsplit** | `bool` | Set to `no` to disable splitting of libraries into `devel` sub-packages
**optimize** | `list` | Specify preset keys to modify compiler and linker flags during build. You can learn more [here](/articles/packaging/package.yml/en/#optimize-values).
**builddeps** | `list` | Specify build dependencies for the package. You can learn more [here](/articles/packaging/packaging-practices/en/#build-dependencies).
**rundeps** | `dict(s)` | Specify further runtime dependencies for the packages. You can learn more [here](/articles/packaging/packaging-practices/en/#runtime-dependencies).
**replaces** | `dict(s)` | Replace one package with another, used when renaming or deprecating packages for clean upgrade paths
**patterns** | `dict(s)` | Allows fine grained control over file placement within the package or sub-packages. Useful for packages that are development only (i.e. `/usr/bin` files)
**environment** | `unicode` | Specify code that will be exported to all build steps of the build (i.e. exporting variables for the entire build).
**networking** | `bool` | Set to `yes` to enable networking within solbuild
**homepage** | `string` | Provides a link to the package's hompage in the software center.

### Build step keys, optional

Note that each step in itself is optional, however all can be used. The value of each of these keys is merged into a build script that is executed for each stage of the build.

Step Name | Description
---- | ----
**setup** | Performed after the source extraction. This is the correct place to perform any `configure` routine, or to `patch` the sources.
**build** | Use this step to run the build portion, i.e. `make`
**install** | This is where you should install the files into the final packaging directory, i.e. `make install`
**check** | This is where tests / checking should occur, i.e. `make check`
**profile** | This is where profiling tests should be specified. `ypkg` will handle setting flags to generate profiling data and using that data for an optimized build.


