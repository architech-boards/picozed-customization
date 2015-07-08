Linux Kernel
============

Like we saw for the :ref:`bootloader <bsp_bootloader_label>`, the first thing you need is: sources.
Get them from *Bitbake* build directory (if you built the kernel with it) or get them from the Internet.

*Bitbake* will place the sources under directory:

.. host::

 | /path/to/build/tmp/work/picozed_zynq7-poky-linux-gnueabi/linux-xlnx/3.14-xilinx+gitAUTOINC+2b48a8aeea-r0


If you are working with the virtual machine, you will find them under directory:

.. host::

 | /home/@user@/architech_sdk/architech/@board-alias@/yocto/build/tmp/work/picozed_zynq7-poky-linux-gnueabi/linux-xlnx/3.14-xilinx+gitAUTOINC+2b48a8aeea-r0


We suggest you to **don't work under Bitbake build directory**, you will pay a speed penalty and you could
have troubles syncronizing the all thing. Just copy them some place else and do what you have to do.

If you didn't build them already with *Bitbake* or you just want to do make every step by hand, you can
always get them from the Internet by cloning the proper repository and checking out the proper hash commit:

.. host::

 | cd ~/Documents
 | git clone -b xlnx_3.14 git://github.com/Xilinx/linux-xlnx.git
 | cd linux-xlnx
 | git checkout 2b48a8aeea7367359f9eebe55c4a09a05227f32b

and by properly patching the sources:

.. host::

 | patch -p1 < ~/architech_sdk/architech/picozed/yocto/meta-picozed/recipes-kernel/linux/linux-xlnx/3.14/picozed.patch
 | patch -p1 < ~/architech_sdk/architech/picozed/yocto/meta-xilinx/recipes-kernel/linux/linux-xlnx/3.14/usb-host-zynq-dr-of-PHY-reset-during-probe.patch
 | patch -p1 < ~/architech_sdk/architech/picozed/yocto/meta-xilinx/recipes-kernel/linux/linux-xlnx/3.14/tty-xuartps-Fix-RX-hang-and-TX-corruption-in-set_termios.patch
 | cp ~/architech_sdk/architech/picozed/yocto/meta-picozed/recipes-kernel/linux/linux-xlnx/3.14/config .config


If you don't use our SDK then use the following commands to patch the sources:

.. host::

 | cd ~/Documents
 | git clone git://git.yoctoproject.org/meta-xilinx.git
 | cd meta-xilinx
 | git checkout 2af8d2a0e63aa371045895da03ba2bf98b51adb4

Source the script to load the proper evironment for the cross-toolchain (see :ref:`manual_compilation_label` Section) and you are ready to customize and compile the kernel:

.. host::
 
 | source ~/architech_sdk/architech/picozed/toolchain/environment-nofs
 | LOADADDR=0x0008000 make uImage -j <2 * number of processor's cores>

Now you need compile the devicetree file:

.. host::

 | make picozed-zynq7.dtb
 
By the end of the build process you will get **uImage** and **devicetree** under *arch/arm/boot*.

.. host::

 ~/Documents/linux-xlnx/arch/arm/boot/uImage
 ~/Documents/linux-xlnx/arch/arm/boot/dts/picozed-zynq7.dtb
 

Enjoy!
