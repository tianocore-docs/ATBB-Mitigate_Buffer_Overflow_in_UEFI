## Limitation {#limitation}

1.  Size

    If the heap page guard is enabled, the core allocates additional 2 pages for each AllocatePages(). If the heap pool guard is enabled, each AllocatePool() becomes AllocatePages(). Even 1 byte allocation need 12K memory. The heap guard feature will increase memory consumption and may cause memory out of resource. Especially, the SMM code runs in the limited SMRAM (4M or 8M).

    We have observed SMRAM out of resource when this feature is turned on. The solution could be:

    *   Enlarge SMRAM

    *   Enable the partial of PageGuard or PoolGuard feature, via gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPageType and gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPoolType PCD.

    *   Enable feature one-by-one. The user can build 2 or more BIOS images, and each image include a subset of full features. For example, if the user wants to detect overflow in USB drivers, there is no need to include network drivers.

2.  Performance

    If the heap guard is enabled, the CPU driver need update the page table for every AllocatePool(), flush TLB (translation lookaside buffer). It brings overhead.

    We have observed the performance downgrade in UEFI Shell, such as DEVTREE command or shell script.

    Some of the performance drop can be resolved by removing the page table synchronization from BSP to APs. When BSP wakes up APs later, the page table is always rewritten. Paging synchronization is unnecessary.

3.  PEI Phase

    The guard in PEI phase is not supported yet, because most IA platforms only supports 32bit PEI and paging is not enabled.

    From technical perspective, we can add paging-based guard after the permanent memory is initialized in PEI. Stack guard, heap guard or NULL pointer detection can be enabled.

    Before the permanent memory is initialize, if we need enabling paging, we can only set paging table on A) Flash Region with Access and Dirty bit set. B) Cache as Ram. C) Static RAM. #A can only support read-only paging, while #B and #C has size limitation.

    In EDKII community, Brian Johnson also provided another way to enable the NULL pointer detection ([https://bugzilla.tianocore.org/show_bug.cgi?id=687](https://bugzilla.tianocore.org/show_bug.cgi?id=687)). We can set “_the GDT descriptor for the data segment from a &quot;extend up&quot; type based at 0, to an &quot;extend down&quot; type with a limit of 0\. This disables access to the 4k page at 0 due to the way the limit math works with &quot;extend down&quot; descriptors._”

4.  Pool Underflow/Overflow detection

    For heap pool detection, we cannot enable both underflow and overflow detection in one image, because the guard page must be 4K aligned and the allocated pool is either adjacent to head guard page or tail guard page.

    In order to detect underflow and overflow, the user must build 2 different images with BIT7 of gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPropertyMask set or cleared.

5.  Emulation Environment

> Current emulation environment (such as NT32) does not have capability to modify CPU page table directly. As such we are not able to enable such page table based protection.
> 
> In the future, we may be able to set up memory for NT32 application process and then use this function to change page protections for pages within that process to match what we have done for the real hardware. For example:

[https://msdn.microsoft.com/en-us/library/windows/desktop/aa366898(v=vs.85).aspx](https://msdn.microsoft.com/en-us/library/windows/desktop/aa366898(v=vs.85).aspx)  

*   BOOL WINAPI VirtualProtect(

*   _In_  LPVOID lpAddress,

*   _In_  SIZE_T dwSize,

*   _In_  DWORD  flNewProtect,

*   _Out_ PDWORD lpflOldProtect

*   ); 

*   FlNewProtect values: [https://msdn.microsoft.com/en-us/library/windows/desktop/aa366786(v=vs.85).aspx](https://msdn.microsoft.com/en-us/library/windows/desktop/aa366786(v=vs.85).aspx)