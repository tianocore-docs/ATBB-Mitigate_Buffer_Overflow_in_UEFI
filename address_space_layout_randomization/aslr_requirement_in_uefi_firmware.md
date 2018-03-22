## ASLR requirement in UEFI firmware {#aslr-requirement-in-uefi-firmware}

The current EDKII code does not support address space randomization. The memory allocation algorithm is top-down. In order to support the randomization in the preboot environment, we define below requirement:

1.  **The randomization algorithm should keep UEFI firmware boot behavior consistent**. If a system has enough memory for boot, it should be able to boot at any time. If a system is out of memory, it should be out of memory for any boot. If a UEFI firmware boots at some time because the memory is enough, but it may fail at some other time because the randomization cause memory being exhausted, then it is not acceptable solution. This is very important for a resource constrained environment, such as SMM or the PEI phase.

2.  **The randomization algorithm should keep OS resume from sleep states required memory being consistent**. An OS may needs to support S4 or S3 resume feature. The OS resume may have some assumption that some special memory is unchanged, such as the runtime memory, or the ACPI memory.

3.  **Any individual component may have its own randomization algorithm.** For example, the GDT, IDT, or Page Table are allocated from heap memory. Even if the heap has randomized, the CPU driver can have additional randomization for GDT/IDT/PageTable specifically.