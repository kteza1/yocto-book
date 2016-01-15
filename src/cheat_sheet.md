##### CLEAN A RECIPE
---
**bitbake -c clean <recipe>**

  
##### FIND AND CHECK PACKAGE CONTENT
---
search here --> **cd tmp/deploy/rpm/**

&

rpm -qlp <package_name>.rpm

**NOTE**: Make sure that you added `IMAGE_INSTALL_append = "<recipe name>"` for package contents to be present in target image rootfs