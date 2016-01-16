##### CLEAN A RECIPE
---
**bitbake -c clean <recipe>**

  
##### FIND AND CHECK PACKAGE CONTENT
---
search here --> **cd tmp/deploy/rpm/**

&

rpm -qlp <package_name>.rpm

**NOTE**: Make sure that you added `IMAGE_INSTALL_append = "<recipe name>"` for package contents to be present in target image rootfs

##### SEARCH BITBAKE ENV
---

**bitbake -e mosquitto | grep ^S=**      --> find src dir of a recipe's package
  
**bitbake -e mosquitto | grep ^WORKDIR** --> find working dir of a package
  
**bitbake -c devshell mosquitto**        --> open dev shell of a recipe

upacks source, patches it and opens recipe dir with environmet correctly set
  
**bitbake -c listtasks mosquitto**       --> list all the tasks of a recipe***
  
**bitbake -c compile -f mosquitto**      --> force compile
  
**bitbake --show-versions | grep mosquitto** --> show package version
  
**bitbake -gu depexp mosquitto**         --> show dependencies