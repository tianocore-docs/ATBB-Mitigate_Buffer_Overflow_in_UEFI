<!--- @file
  Additional Overflow Detection file: -Heap Overflow Detection (for Pool)

  Copyright (c) 2018, Intel Corporation. All rights reserved.<BR>

  Redistribution and use in source (original document form) and 'compiled'
  forms (converted to PDF, epub, HTML and other formats) with or without
  modification, are permitted provided that the following conditions are met:

  1) Redistributions of source code (original document form) must retain the
     above copyright notice, this list of conditions and the following
     disclaimer as the first lines of this file unmodified.

  2) Redistributions in compiled form (transformed to other DTDs, converted to
     PDF, epub, HTML and other formats) must reproduce the above copyright
     notice, this list of conditions and the following disclaimer in the
     documentation and/or other materials provided with the distribution.

  THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR
  IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
  MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO
  EVENT SHALL TIANOCORE PROJECT  BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
  SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
  PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS;
  OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
  WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR
  OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF
  ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

-->

## Heap Overflow Detection (for Pool) {#heap-overflow-detection-for-pool}

We can use GuardPage for pages. What about pool?

If the pool guard is enabled, each pool allocation becomes the page allocation with the guarded page. Because the pool size might not be a multiple of the page size, we can only set guard page at the head of pool or at the tail of pool. This behavior is controlled by `BIT7` of `gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPropertyMask`. By default the returned pool is near the tail guard page to check overflow. If the `BIT7` is set, the returned pool is near the head guard page to check underflow. See figure 4-11.

![](/media/image26.png)

###### Figure 4-11 HeapGuard for Pool Overflow Detection

This enhancement for the guarded pool is in [https://github.com/tianocore/edk2/blob/master/MdeModulePkg/Core/Dxe/Mem/Pool.c](https://github.com/tianocore/edk2/blob/master/MdeModulePkg/Core/Dxe/Mem/Pool.c). If the `IsPoolTypeToGuard()` returns TRUE, `CoreAllocatePoolI()` uses `CoreAllocatePoolPagesI()` directly to allocate pages for pool with the guarded pages. In the last step, `SetGuardForMemory()` is invoked to set the guard page around the allocated pool.