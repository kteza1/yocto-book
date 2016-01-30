## HOW BUILD WORKS
---

`oe-init-build` script calls the `scripts/oe-setup-builddir` script inside the poky directory to create the build directory. 

On creation, the build directory contains a conf directory with the following three files: 

* **bblayers.conf**: This file lists the metadata layers to be considered for this project. 
* **local.conf**: This file contains the project-specific configuration variables. You can set common configuration variables to different projects with a site.conf file, but this is not created by default. 
* **templateconf.cfg**: This file contains the directory that includes the template configuration files used to create the project. By default it uses the one pointed to by the templateconf file in your Poky installation directory, which is meta-yocto/conf by default

Removing these will start the build from scratch

```
$ cd /opt/yocto/poky/<build dir>
$ rm -Rf tmp sstate-cache
```

#### CHOOSING A CUSTOM TEMPLATE CONFIGURATION

when you create your build directory using the `TEMPLATECONF` variable; for example

```
$ TEMPLATECONF=meta-custom/config source oe-init-build-env <build- dir> 
```

The `TEMPLATECONF` variable needs to refer to a directory containing templates for both local.conf and bblayer.conf, but named `local.conf.sample` and `bblayers.conf.sample`


#### BUILD CONFIG
---

Choose the image that you want to build for. Poky has support for some **image configurations** by default

```
$ cd /opt/yocto/poky 
$ ls meta*/recipes*/images/*.bb
```


#### DIFFERENT IMAGE CONFIG SUFFIXES

* **dev**: These images are suitable for development work, as they contain headers and libraries. 
* **sdk**: These images include a complete SDK that can be used for development on the target
* **initramfs**: This is an image that can be used for a RAM-based root filesystem, which can optionally be embedded with the Linux kernel

#### STARTING THE BUILD
---

```
$ cd /opt/yocto/poky
$ source oe-init-build-env qemuarm
$ MACHINE=qemuarm bitbake core-image-minimal
```

#### HOW IT WORKS
---

When you pass a target recipe (**core-image-minimal.bb**) to BitBake, it first parses the following configuration files: 

* **<build dir>/conf/bblayers.conf**: This file is used to find all the configured layers 
* **meta/conf/layer.conf**: This file is used on each configured layer 
* **meta/conf/bitbake.conf**: This file is used for its own configuration 
* **<build dir>/conf/local.conf**: This file is used for any other configuration the user may have for the current build 
* **meta/conf/machine/<machine>.conf**: This file is the machine configuration; in our case, this is `qemuarm.conf`
* **meta-yocto/conf/distro/<distro>.conf**: This file is the distribution policy; by default, this is the `poky.conf` file

And then BitBake parses the **target recipe** that has been provided and its dependencies. The outcome is a set of interdependent tasks that BitBake will then execute in order

#### TIP 1

Most developers won't be interested in keeping the whole build output for every package, so it is recommended to configure your project to remove it with the following configuration in your `conf/local.conf` file: 

```
INHERIT += "rm_work" 
```

But at the same time, configuring it for all packages means that you won't be able to develop or debug them. You can add a list of packages to exclude from cleaning by adding them to the `RM_WORK_EXCLUDE` variable. For example, if you are going to do BSP work, a good setting might be: 

```
RM_WORK_EXCLUDE += "linux-yocto u-boot"
```

#### TIP 2

You can use a `custom template` config `local.conf.sample` configuration file in your own layer to keep these configurations and apply them for all projects so that they can be shared across all developers. Use the `TEMPLATECONF` var


#### IMAGES
---

You can find images here

```
tmp/deploy/images/qemuarm
```

directory inside your build directory

#### TIP

By default, images are not erased from the deploy directory, but you can configure your project to remove the previously built version of the same image by adding the following to your `conf/local.conf` file: 

```
RM_OLD_IMAGE = "1"
```


### RUN THE IMAGE
---

```
$ runqemu qemuarm core-image-minimal
```

