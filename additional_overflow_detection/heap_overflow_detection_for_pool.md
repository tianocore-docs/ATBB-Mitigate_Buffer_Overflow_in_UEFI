## Heap Overflow Detection (for Pool) {#heap-overflow-detection-for-pool}

We can use GuardPage for pages. What about pool?

If the pool guard is enabled, each pool allocation becomes the page allocation with the guarded page. Because the pool size might not be a multiple of the page size, we can only set guard page at the head of pool or at the tail of pool. This behavior is controlled by BIT7 of gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPropertyMask. By default the returned pool is near the tail guard page to check overflow. If the BIT7 is set, the returned pool is near the head guard page to check underflow. See figure 4-11.

![](Mydir/media/image26.png)

Figure 4-11 HeapGuard for Pool Overflow Detection

This enhancement for the guarded pool is in [https://github.com/tianocore/edk2/blob/master/MdeModulePkg/Core/Dxe/Mem/Pool.c](https://github.com/tianocore/edk2/blob/master/MdeModulePkg/Core/Dxe/Mem/Pool.c). If the IsPoolTypeToGuard() returns TRUE, CoreAllocatePoolI() uses CoreAllocatePoolPagesI() directly to allocate pages for pool with the guarded pages. In the last step, SetGuardForMemory() is invoked to set the guard page around the allocated pool.