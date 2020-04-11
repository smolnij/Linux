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


#### Kernel parameters
Checkout here:  https://github.com/clearlinux-pkgs/linux/blob/master/cmdline


With no console parameter the kernel will use the first virtual terminal, which is /dev/tty0. A user at the keyboard uses this virtual terminal by pressing Ctrl-Alt-F1.
If your computer contains a video card then we suggest that you also configure it as a console. This is done with the kernel parameter console=tty0.
console=tty0
Kernel messages will appear on both the first virtual terminal and the serial port. Messages from the init system and the system logger will appear only on the first serial port. This can be slightly confusing when looking at the attached monitor: the machine will appear to boot and then hang. Don't panic, the init system has started but is now printing messages to the serial port but is printing nothing to the screen. If a getty has been configured then a login: prompt will eventually appear on the attached monitor.


cryptomgr.notests
   [KNL] Disable crypto self-tests

no_timer_check
 [X86,APIC] Disables the code which tests for
                        broken timer IRQ sources.
						
						
noreplace-smp				
+ * The SMP alternative tables can be kept after boot and contain both
+ * UP and SMP versions of the instructions to allow switching back to
+ * SMP at runtime, when hotplugging in a new CPU, which is especially
+ * useful in virtualized environments.		


page_alloc.shuffle=1 
 Randomization of the page allocator improves the average
> > +       utilization of a direct-mapped memory-side-cache. See section
> > +       5.2.27 Heterogeneous Memory Attribute Table (HMAT) in the ACPI
> > +       6.2a specification for an example of how a platform advertises
> > +       the presence of a memory-side-cache. There are also incidental
> > +       security benefits as it reduces the predictability of page
> > +       allocations to compliment SLAB_FREELIST_RANDOM, but the
> > +       default granularity of shuffling on 4MB (MAX_ORDER) pages is
> > +       selected based on cache utilization benefits.
> > +
> > +       While the randomization improves cache utilization it may
> > +       negatively impact workloads on platforms without a cache. For
> > +       this reason, by default, the randomization is enabled only
> > +       after runtime detection of a direct-mapped memory-side-cache.
> > +       Otherwise, the randomization may be force enabled with the
> > +       'page_alloc.shuffle' kernel command line parameter.


rcu_nocbs=0-64
https://utcc.utoronto.ca/~cks/space/blog/linux/KernelRcuNocbsMeaning
rcu_nocbs=0-N
where N is the number of CPUs you have minus one
However, the rcu_nocbs=0-N setting we're using specifies all CPUs, so it shifts all RCU callbacks from softirq context during interrupt handling (on whatever specific CPU involved) to kernel threads (on any CPU). As far as I can see, this has two potentially significant effects, given that Matt Dillon of DragonFly BSD has reported an issue with IRETQ that completely stops a CPU under some circumstances. First, our Ryzen CPUs will spend less time in interrupt handling, possibly much less time, which may narrow any timing window required to hit Matt Dillon's issue. Second, RCU callback processing will continue even if a CPU stops responding to IPIs, although I expect that a CPU not responding to IPIs is going to cause the Linux kernel various other sorts of heartburn.

rw 
mount root device readwrite on boot




Passing the option "initcall_debug" on the kernel command line will cause timing information to be printed to the console for each initcall. initcalls are used to initialize statically linked kernel drivers and subsystems and contribute a significant amount of time to the Linux boot process. The output looks like this:

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
