# INTRODUCTION

poky is the build system for yocto

**poky = bitbake + open embedded core**

poky builds following components

1. bootloader image
2. linux kernel image
3. root fs image
4. toolchais and SDKs for application development

1 + 2 + 3 => system development
4         => for application development

Openwrt took buildroot approach of makefiles + kconfig while openembedded took a different approach

OpenEmbedded recipes can specify dependencies between packages, and later on, **BitBake parses all the recipes and creates a queue of tasks in the correct order to fulfill the dependencies**

Two examples of distributions created with OpenEmbedded are Angstrom and OpenMoko. Another OpenEmbedded-based distribution was Poky


