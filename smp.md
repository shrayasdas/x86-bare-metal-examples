# SMP

# Symmetric multiprocessing

-   Intel docs: Volume 3, Chapter 8 "Multiple processor Management".

    Does not seem standardized across to AMD.

    On Intel goes through the APIC to generate an interrupt across processors:

    > Wait-for-SIPI. As part of its initialization, the primary thread sends a special inter-processor-interrupt (IPI) over the APIC called a SIPI (Startup IPI) to each thread that is in WFS. The SIPI contains the address from which that thread should start fetching code.

-   https://en.wikipedia.org/wiki/Inter-processor_interrupt

-   Linux kernel `arch/x86/kernel/smpboot.c`

-   newer Intel processors have an L2 shared across cores:

    - http://stackoverflow.com/questions/4802565/multiple-threads-and-cpu-cache
    - http://stackoverflow.com/questions/944966/cache-memories-in-multicore-cpus
    - http://programmers.stackexchange.com/questions/183686/can-multiple-cpus-cores-access-the-same-ram-simutaneously

    Intel calls this "Intel® Smart Cache".

-   http://superuser.com/questions/700430/what-does-2-core-4-threads-mean-in-cpu

-   The real reason why multicore exists: too much heat: https://en.wikipedia.org/wiki/Dennard_scaling

-   MIC many integrated cores: Intel name for the type of architecture of the Xeon Phi

    http://www.intel.com/content/www/us/en/architecture-and-technology/many-integrated-core/intel-many-integrated-core-architecture.html

    GPU competitor basically.

    One huge advantage: Phi is programmed with x86!

    - <http://stackoverflow.com/questions/7353136/is-there-an-assembly-language-for-cuda>
    - <http://superuser.com/questions/668019/how-do-device-driver-instructions-program-the-gpu>

Nice quotes from Intel:

> The MP initialization protocol defines two classes of processors: the bootstrap processor (BSP) and the application
processors (APs). Following a power-up or RESET of an MP system, system hardware dynamically selects one of the
processors on the system bus as the BSP. The remaining processors are designated as APs.

> Following a power-up or reset, the APs complete a minimal self-configuration, then wait for a startup signal (a SIPI
message) from the BSP processor. Upon receiving a SIPI message, an AP executes the BIOS AP configuration code,
which ends with the AP being placed in halt state.