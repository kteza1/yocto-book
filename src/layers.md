# LAYERS

Poky contains three metadata directories, meta, meta-yocto, and meta-yocto-bsp, as well as a template metadata layer, meta-skeleton, that can be used as a base for new layers

* **meta**: This directory contains the OpenEmbedded-Core metadata, which supports the ARM, x86, x86-64, PowerPC, MIPS, and MIPS64 architectures and the QEMU emulated hardware.
* **meta-yocto**: This contains Poky's distribution-specific metadata.
* **meta-yocto-bsp**: This contains metadata for the reference hardware boards