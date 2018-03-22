## Call for action {#call-for-action}

1.  Enable the **Stack Overflow detection** to catch stack overflow (especially in SMM)

    1.  gEfiMdeModulePkgTokenSpaceGuid.PcdCpuStackGuard

    2.  gUefiCpuPkgTokenSpaceGuid.PcdCpuSmmStackGuard

2.  Enable the **Heap Overflow detection** in a debug BIOS to catch potential buffer overflow issue.

    1.  gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPageType

    2.  gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPoolType

    3.  gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPropertyMask

3.  Enable the **NULL pointer detection** to catch the NULL address access.

    1.  gEfiMdeModulePkgTokenSpaceGuid.PcdNullPointerDetectionPropertyMask