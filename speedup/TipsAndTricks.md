## To cover here:


#### LZO vs LZ4 compression

#### LZO/LZ4 compression for kernel & modules

open /etc/mkinicpio.conf, add
COMPRESION ="LZ4", bu default gzip is used
regenerate 
mkinitcpio -p linux


#### LZO/LZ4 compression for F2FS fs

#### LTO optimisation

#### GRUB loadmodule GPT/MBR exclusion

#### GRUB early load

#### Minimal initramfs

#### Skip initramfs

The key to this technique for booting your kernel is the rootfstype=ext4 kernel command line argument which enables a user to force mount the root filesystem of a given type. This option allows you to give a comma separated list of filesystem types that will be tried for a match when trying to mount the root filesystem. This list will be used instead of the internal default. Internally, initramfs typically sets rootfstype to auto.


Read more: https://blog.fpmurphy.com/2013/08/boot-linux-without-an-initramfs-2.html#ixzz6ECxZggMY


#### Kernel config & build

#### Kernel parameters
Disable mitigations
i915.enable_fbc=1 
fastboot=1
rootfstype=f2fs
noinitrd ???

#### CFLAGS

 -fexcess-precision=fast
  Если для Вашего Atom приложения важен и размер кода, и производительность — переключайтесь на GCC версии 4.8 и пробуйте компилировать с опциями:
“-O2 -ffast-math -mfpmath=sse -ftree-loop-if-convet -fschedule-insns -fsched-pressure -march=bonnell”
comment out debug flags?

#### Kernel config & build
#### dbus-broker instead of D-Bus

#### Microcode


You might not need microcode updates. You can check if your cpu is actually present in the microcode image.

Detecting available microcode update

It is possible to find out if the intel-ucode.img contains a microcode image for the running CPU with iucode-tool.

    Install intel-ucode (changing initrd is not required for detection)
    Install iucode-tool

    # modprobe cpuid

    Extract microcode image and search it for your cpuid:

    # bsdtar -Oxf /boot/intel-ucode.img | iucode_tool -tb -lS -

    If an update is available, it should show up below selected microcodes
    The microcode might already be in your vendor bios and not show up loading in dmesg. Compare to the current microcode running grep microcode /proc/cpuinfo


Another way to check it, is to install microcode package and check dmesg

[    0.000000] CPU0 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.221951] CPU1 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.242064] CPU2 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.262349] CPU3 microcode updated early to revision 0x1b, date = 2014-05-29


If you don't see the messages regarding microcode update, just microcode driver or so, your cpu don't need it, so skipping this extra step will speed up loading time.
