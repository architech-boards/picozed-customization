Meta Layer
==========

A Yocto/OpenEmbedded meta-layer is a directory that contains recipes, configuration files, patches, etc., all needed by
*Bitbake* to properly "see" and build a BSP, a distribution, a (set of) package(s), whatever.
**@meta-layer@** is a meta-layer which defines the BSP for Microzed device, @board@ included. 
You can get it with *git*:

.. host::

 | git clone -b dizzy https://github.com/architech-boards/meta-microzed.git

This layer depends with this one which defines the BSP for Xilinx devices:

 | git clone git://git.yoctoproject.org/meta-xilinx.git
 | cd meta-xilinx/
 | git checkout 2af8d2a0e63aa371045895da03ba2bf98b51adb4

Please, refer to the *README* file contained inside the meta-layer directory.

The machine name corresponding to @board@ is **@machine-name@**.
