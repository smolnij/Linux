## To cover here:


#### LZO vs LZ4 compression

#### LZO/LZ4 compression for kernel

#### LZO compression for F2FS fs

#### LTO optimisation

#### GRUB loadmodule GPT/MBR exclusion

#### GRUB early load

#### Minimal initramfs

#### Skip initramfs


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

#### Disable mitigations

#### CFLAGS
 -fexcess-precision=fast
  Если для Вашего Atom приложения важен и размер кода, и производительность — переключайтесь на GCC версии 4.8 и пробуйте компилировать с опциями:
“-O2 -ffast-math -mfpmath=sse -ftree-loop-if-convet -fschedule-insns -fsched-pressure -march=bonnell”

#### Kernel config & build

#### dbus-broker instead of D-Bus

#### HW video acceleration

Intel does not offer VDPAU drivers, they only support their VA-API. It is, however, possible to use Intel's VA-API drivers by way of libvdpau-va-gl.



#### Other features
Intel rapid start https://askubuntu.com/questions/699615/how-to-setup-intel-rapid-start
https://www.intel.com/content/dam/www/public/us/en/documents/white-papers/rst-linux-paper.pdf


#### Browsers
NetSurf
Midori
Palemoon
Firefox tricks
dom.image-lazy-loading.enabled=true

### IO Schdeuler
https://www.phoronix.com/scan.php?page=article&item=linux-56-nvme&num=4
Overall though, using "none" as your I/O scheduler option will still generally offer the best performance for speedy NVMe SSD storage with a few exceptions. Similar tests on SATA HDD/SSDs off Linux 5.6 coming up shortly on Phoronix.