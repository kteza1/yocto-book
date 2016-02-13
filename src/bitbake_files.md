> DEPENDS means a build-time dependency i.e. between recipes, RDEPENDS means a
> runtime dependency i.e. between packages. It is worth noting though that an
> explicitly stated RDEPENDS will cause bitbake to actually build the recipe
> providing the package named in the RDEPENDS value, just at a different time. To
> explain exactly what each of these do:
>
> * DEPENDS = "b" in recipe "a" will translate to a's do_configure task depending
> on recipe b's do_populate_sysroot task, so that anything recipe b puts into
> the sysroot is available for when a configures itself.
>
> * RDEPENDS_${PN} = "b" in recipe "a" will translate to a's do_build task
> depending on recipe b's do_package_write task, so that the package file b is
> available when the output for a has been completely built (of course assuming
> that recipe b produces a package called "b", which it will with the default
> value of PACKAGES). More importantly it will also ensure that package "a" is
> marked as depending on "b" in a manner understood by the package manager being
> used e.g. rpm / opkg / dpkg.
