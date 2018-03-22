<!--- @file
  Summary File: - Policy Control

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
## Policy Control {#policy-control}

### Stack Guard: _Detect Stack Overflow_ {#stack-guard-detect-stack-overflow}
```
gEfiMdeModulePkgTokenSpaceGuid.PcdCpuStackGuard
  ## Indicates if UEFI Stack Guard will be enabled.
  #  If enabled, stack overflow in UEFI can be caught, preventing chaotic consequences.<BR><BR>
  #   TRUE  - UEFI Stack Guard will be enabled.<BR>
  #   FALSE - UEFI Stack Guard will be disabled.<BR>

gUefiCpuPkgTokenSpaceGuid.PcdCpuSmmStackGuard
  ## Indicates if SMM Stack Guard will be enabled.
  #  If enabled, stack overflow in SMM can be caught, preventing chaotic consequences.<BR><BR>
  #   TRUE  - SMM Stack Guard will be enabled.<BR>
  #   FALSE - SMM Stack Guard will be disabled.<BR>
```

### NULL pointer detection: _Detect NULL pointer access_ {#null-pointer-detection-detect-null-pointer-access}

```
gEfiMdeModulePkgTokenSpaceGuid.PcdNullPointerDetectionPropertyMask
  ## Mask to control the NULL address detection in code for different phases.
  #  If enabled, accessing NULL address in UEFI or SMM code can be caught.<BR><BR>
  #    BIT0    - Enable NULL pointer detection for UEFI.<BR>
  #    BIT1    - Enable NULL pointer detection for SMM.<BR>
  #    BIT2..6 - Reserved for future uses.<BR>
  #    BIT7    - Disable NULL pointer detection just after EndOfDxe. <BR>
  #              This is a workaround for those unsolvable NULL access issues in
  #              OptionROM, boot loader, etc. It can also help to avoid unnecessary
  #              exception caused by legacy memory (0-4095) access after EndOfDxe,
  #              such as Windows 7 boot on Qemu.<BR>
```



### Heap Guard: _Detect Heap Overflow._ {#heap-guard-detect-heap-overflow}

```
gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPageType
  ## Indicates which type allocation need guard page.
  #
  # If a bit is set, a head guard page and a tail guard page will be added just
  # before and after corresponding type of pages allocated if there's enough
  # free pages for all of them. The page allocation for the type related to
  # cleared bits keeps the same as ususal.
  #
  # Below is bit mask for this PCD: (Order is same as UEFI spec)<BR>
  #  EfiReservedMemoryType             0x0000000000000001<BR>
  #  EfiLoaderCode                     0x0000000000000002<BR>
  #  EfiLoaderData                     0x0000000000000004<BR>
  #  EfiBootServicesCode               0x0000000000000008<BR>
  #  EfiBootServicesData               0x0000000000000010<BR>
  #  EfiRuntimeServicesCode            0x0000000000000020<BR>
  #  EfiRuntimeServicesData            0x0000000000000040<BR>
  #  EfiConventionalMemory             0x0000000000000080<BR>
  #  EfiUnusableMemory                 0x0000000000000100<BR>
  #  EfiACPIReclaimMemory              0x0000000000000200<BR>
  #  EfiACPIMemoryNVS                  0x0000000000000400<BR>
  #  EfiMemoryMappedIO                 0x0000000000000800<BR>
  #  EfiMemoryMappedIOPortSpace        0x0000000000001000<BR>
  #  EfiPalCode                        0x0000000000002000<BR>
  #  EfiPersistentMemory               0x0000000000004000<BR>
  #  OEM Reserved                      0x4000000000000000<BR>
  #  OS Reserved                       0x8000000000000000<BR>
  # e.g. LoaderCode+LoaderData+BootServicesCode+BootServicesData are needed, 0x1E should be used.<BR>

gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPoolType
  ## Indicates which type allocation need guard page.
  #
  # If a bit is set, a head guard page and a tail guard page will be added just
  # before and after corresponding type of pages which the allocated pool occupies,
  # if there's enough free memory for all of them. The pool allocation for the
  # type related to cleared bits keeps the same as ususal.
  #
  # Below is bit mask for this PCD: (Order is same as UEFI spec)<BR>
  #  EfiReservedMemoryType             0x0000000000000001<BR>
  #  EfiLoaderCode                     0x0000000000000002<BR>
  #  EfiLoaderData                     0x0000000000000004<BR>
  #  EfiBootServicesCode               0x0000000000000008<BR>
  #  EfiBootServicesData               0x0000000000000010<BR>
  #  EfiRuntimeServicesCode            0x0000000000000020<BR>
  #  EfiRuntimeServicesData            0x0000000000000040<BR>
  #  EfiConventionalMemory             0x0000000000000080<BR>
  #  EfiUnusableMemory                 0x0000000000000100<BR>
  #  EfiACPIReclaimMemory              0x0000000000000200<BR>
  #  EfiACPIMemoryNVS                  0x0000000000000400<BR>
  #  EfiMemoryMappedIO                 0x0000000000000800<BR>
  #  EfiMemoryMappedIOPortSpace        0x0000000000001000<BR>
  #  EfiPalCode                        0x0000000000002000<BR>
  #  EfiPersistentMemory               0x0000000000004000<BR>
  #  OEM Reserved                      0x4000000000000000<BR>
  #  OS Reserved                       0x8000000000000000<BR>
  # e.g. LoaderCode+LoaderData+BootServicesCode+BootServicesData are needed, 0x1E should be used.<BR>

gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPropertyMask
  ## This mask is to control Heap Guard behavior.
  # Note that due to the limit of pool memory implementation and the alignment
  # requirement of UEFI spec, BIT7 is a try-best setting which cannot guarantee
  # that the returned pool is exactly adjacent to head guard page or tail guard
  # page.
  #   BIT0 - Enable UEFI page guard.<BR>
  #   BIT1 - Enable UEFI pool guard.<BR>
  #   BIT2 - Enable SMM page guard.<BR>
  #   BIT3 - Enable SMM pool guard.<BR>
  #   BIT7 - The direction of Guard Page for Pool Guard.
  #          0 - The returned pool is near the tail guard page.<BR>
  #          1 - The returned pool is near the head guard page.<BR>


```


### Memory Profile: _Provide memory usage information, detect memory leak_ {#memory-profile-provide-memory-usage-information-detect-memory-leak}
```
gEfiMdeModulePkgTokenSpaceGuid.PcdMemoryProfilePropertyMask
  ## The mask is used to control memory profile behavior.<BR><BR>
  #  BIT0 - Enable UEFI memory profile.<BR>
  #  BIT1 - Enable SMRAM profile.<BR>
  #  BIT7 - Disable recording at the start.<BR>

gEfiMdeModulePkgTokenSpaceGuid.PcdMemoryProfileMemoryType
  ## This flag is to control which memory types of alloc info will be recorded by DxeCore & SmmCore.<BR><BR>
  # For SmmCore, only EfiRuntimeServicesCode and EfiRuntimeServicesData are valid.<BR>
  #
  # Below is bit mask for this PCD: (Order is same as UEFI spec)<BR>
  #  EfiReservedMemoryType          0x0001<BR>
  #  EfiLoaderCode                  0x0002<BR>
  #  EfiLoaderData                  0x0004<BR>
  #  EfiBootServicesCode            0x0008<BR>
  #  EfiBootServicesData            0x0010<BR>
  #  EfiRuntimeServicesCode         0x0020<BR>
  #  EfiRuntimeServicesData         0x0040<BR>
  #  EfiConventionalMemory          0x0080<BR>
  #  EfiUnusableMemory              0x0100<BR>
  #  EfiACPIReclaimMemory           0x0200<BR>
  #  EfiACPIMemoryNVS               0x0400<BR>
  #  EfiMemoryMappedIO              0x0800<BR>
  #  EfiMemoryMappedIOPortSpace     0x1000<BR>
  #  EfiPalCode                     0x2000<BR>
  #  EfiPersistentMemory            0x4000<BR>
  #  OEM Reserved       0x4000000000000000<BR>
  #  OS Reserved        0x8000000000000000<BR>
  #
  # e.g. Reserved+ACPINvs+ACPIReclaim+RuntimeCode+RuntimeData are needed, 0x661 should be used.<BR>

gEfiMdeModulePkgTokenSpaceGuid.PcdMemoryProfileDriverPath
  ## This PCD is to control which drivers need memory profile data.<BR><BR>
  # For example:<BR>
  # One image only (Shell):<BR>
  #     Header                    GUID<BR>
  #     {0x04, 0x06, 0x14, 0x00,  0x83, 0xA5, 0x04, 0x7C, 0x3E, 0x9E, 0x1C, 0x4F, 0xAD, 0x65, 0xE0, 0x52, 0x68, 0xD0, 0xB4, 0xD1,<BR>
  #      0x7F, 0xFF, 0x04, 0x00}<BR>
  # Two or more images (Shell + WinNtSimpleFileSystem):<BR>
  #     {0x04, 0x06, 0x14, 0x00,  0x83, 0xA5, 0x04, 0x7C, 0x3E, 0x9E, 0x1C, 0x4F, 0xAD, 0x65, 0xE0, 0x52, 0x68, 0xD0, 0xB4, 0xD1,<BR>
  #      0x7F, 0x01, 0x04, 0x00,<BR>
  #      0x04, 0x06, 0x14, 0x00,  0x8B, 0xE1, 0x25, 0x9C, 0xBA, 0x76, 0xDA, 0x43, 0xA1, 0x32, 0xDB, 0xB0, 0x99, 0x7C, 0xEF, 0xEF,<BR>
  #      0x7F, 0xFF, 0x04, 0x00}<BR>

```

### NX stack: _Prevent code execution in stack_ {#nx-stack-prevent-code-execution-in-stack}

```
gEfiMdeModulePkgTokenSpaceGuid.PcdSetNxForStack
  ## Indicates if to set NX for stack.<BR><BR>
  #  For the DxeIpl and the DxeCore are both X64, set NX for stack feature also require PcdDxeIplBuildPageTables be TRUE.<BR>
  #  For the DxeIpl and the DxeCore are both IA32 (PcdDxeIplSwitchToLongMode is FALSE), set NX for stack feature also require
  #  IA32 PAE is supported and Execute Disable Bit is available.<BR>
  #   TRUE  - to set NX for stack.<BR>
  #   FALSE - Not to set NX for stack.<BR>
```

### DXE NX/RO Protection: _Prevent code injection_ {#dxe-nx-ro-protection-prevent-code-injection}




### DXE image Protection: _Prevent code injection_ {#dxe-image-protection-prevent-code-injection}



### SMM static paging: _Provide code injection in SMM_ {#smm-static-paging-provide-code-injection-in-smm}

### SMI Handler Profile: _Provide SMI handler information_ {#smi-handler-profile-provide-smi-handler-information}
