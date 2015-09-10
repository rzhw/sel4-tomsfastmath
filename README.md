# seL4 TomsFastMath

[TomsFastMath](https://github.com/libtom/tomsfastmath) as a seL4 library.

## Details

`src/` contains the TomsFastMath 0.12 source, and `Kbuild`, `Kconfig`, and
`Makefile` files are included to support the seL4 build system.

## Usage

### Dependencies

This library assumes the existence of [seL4/libmuslc](https://github.com/seL4/libmuslc).

### Repo manifest

Add the remote:

    <remote name="rzhw" fetch="ssh://git@github.com/rzhw/" />

Add the library as `libtomsfastmath`:

    <project name="sel4-tomsfastmath.git" path="libs/libtomsfastmath" />

### Build system

Add it to your root `Kconfig`:

    menu "seL4 Libraries"
        ...
        source "libs/libtomsfastmath/Kconfig"
        ...
    endmenu

Add it to your app/lib `Kbuild`, for example:

    libs-$(CONFIG_LIB_MOPED) += libmoped
    libmoped: common $(libc) libtomsfastmath

Add it to your app/lib `Kconfig`, for example:

    config LIB_MOPED
        bool "Moped"
        depends on HAVE_LIBC && LIB_TOMSFASTMATH
        default y
        help
            You don't want no beef boy

You might need to include it in your app `Makefile`, for example:

    LIBS = c sel4 cpio elf sel4muslcsys sel4vka sel4allocman \
           platsupport sel4platsupport sel4test sel4vspace \
           sel4utils sel4simple utils tomsfastmath
