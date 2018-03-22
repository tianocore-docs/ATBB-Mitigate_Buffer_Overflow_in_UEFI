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

**gEfiMdeModulePkgTokenSpaceGuid.PcdCpuStackGuard**

## Indicates if UEFI Stack Guard will be enabled.

# If enabled, stack overflow in UEFI can be caught, preventing chaotic consequences.&lt;BR&gt;&lt;BR&gt;

# TRUE - UEFI Stack Guard will be enabled.&lt;BR&gt;

# FALSE - UEFI Stack Guard will be disabled.&lt;BR&gt;

**gUefiCpuPkgTokenSpaceGuid.PcdCpuSmmStackGuard**

## Indicates if SMM Stack Guard will be enabled.

# If enabled, stack overflow in SMM can be caught, preventing chaotic consequences.&lt;BR&gt;&lt;BR&gt;

# TRUE - SMM Stack Guard will be enabled.&lt;BR&gt;

# FALSE - SMM Stack Guard will be disabled.&lt;BR&gt;

### NULL pointer detection: _Detect NULL pointer access_ {#null-pointer-detection-detect-null-pointer-access}

**gEfiMdeModulePkgTokenSpaceGuid.PcdNullPointerDetectionPropertyMask**

## Mask to control the NULL address detection in code for different phases.

# If enabled, accessing NULL address in UEFI or SMM code can be caught.&lt;BR&gt;&lt;BR&gt;

# BIT0 - Enable NULL pointer detection for UEFI.&lt;BR&gt;

# BIT1 - Enable NULL pointer detection for SMM.&lt;BR&gt;

# BIT2..6 - Reserved for future uses.&lt;BR&gt;

# BIT7 - Disable NULL pointer detection just after EndOfDxe. &lt;BR&gt;

# This is a workaround for those unsolvable NULL access issues in

# OptionROM, boot loader, etc. It can also help to avoid unnecessary

# exception caused by legacy memory (0-4095) access after EndOfDxe,

# such as Windows 7 boot on Qemu.&lt;BR&gt;

### Heap Guard: _Detect Heap Overflow._ {#heap-guard-detect-heap-overflow}

**gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPageType**

## Indicates which type allocation need guard page.

#

# If a bit is set, a head guard page and a tail guard page will be added just

# before and after corresponding type of pages allocated if there&#039;s enough

# free pages for all of them. The page allocation for the type related to

# cleared bits keeps the same as ususal.

#

# Below is bit mask for this PCD: (Order is same as UEFI spec)&lt;BR&gt;

# EfiReservedMemoryType 0x0000000000000001&lt;BR&gt;

# EfiLoaderCode 0x0000000000000002&lt;BR&gt;

# EfiLoaderData 0x0000000000000004&lt;BR&gt;

# EfiBootServicesCode 0x0000000000000008&lt;BR&gt;

# EfiBootServicesData 0x0000000000000010&lt;BR&gt;

# EfiRuntimeServicesCode 0x0000000000000020&lt;BR&gt;

# EfiRuntimeServicesData 0x0000000000000040&lt;BR&gt;

# EfiConventionalMemory 0x0000000000000080&lt;BR&gt;

# EfiUnusableMemory 0x0000000000000100&lt;BR&gt;

# EfiACPIReclaimMemory 0x0000000000000200&lt;BR&gt;

# EfiACPIMemoryNVS 0x0000000000000400&lt;BR&gt;

# EfiMemoryMappedIO 0x0000000000000800&lt;BR&gt;

# EfiMemoryMappedIOPortSpace 0x0000000000001000&lt;BR&gt;

# EfiPalCode 0x0000000000002000&lt;BR&gt;

# EfiPersistentMemory 0x0000000000004000&lt;BR&gt;

# OEM Reserved 0x4000000000000000&lt;BR&gt;

# OS Reserved 0x8000000000000000&lt;BR&gt;

# e.g. LoaderCode+LoaderData+BootServicesCode+BootServicesData are needed, 0x1E should be used.&lt;BR&gt;

**gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPoolType**

## Indicates which type allocation need guard page.

#

# If a bit is set, a head guard page and a tail guard page will be added just

# before and after corresponding type of pages which the allocated pool occupies,

# if there&#039;s enough free memory for all of them. The pool allocation for the

# type related to cleared bits keeps the same as ususal.

#

# Below is bit mask for this PCD: (Order is same as UEFI spec)&lt;BR&gt;

# EfiReservedMemoryType 0x0000000000000001&lt;BR&gt;

# EfiLoaderCode 0x0000000000000002&lt;BR&gt;

# EfiLoaderData 0x0000000000000004&lt;BR&gt;

# EfiBootServicesCode 0x0000000000000008&lt;BR&gt;

# EfiBootServicesData 0x0000000000000010&lt;BR&gt;

# EfiRuntimeServicesCode 0x0000000000000020&lt;BR&gt;

# EfiRuntimeServicesData 0x0000000000000040&lt;BR&gt;

# EfiConventionalMemory 0x0000000000000080&lt;BR&gt;

# EfiUnusableMemory 0x0000000000000100&lt;BR&gt;

# EfiACPIReclaimMemory 0x0000000000000200&lt;BR&gt;

# EfiACPIMemoryNVS 0x0000000000000400&lt;BR&gt;

# EfiMemoryMappedIO 0x0000000000000800&lt;BR&gt;

# EfiMemoryMappedIOPortSpace 0x0000000000001000&lt;BR&gt;

# EfiPalCode 0x0000000000002000&lt;BR&gt;

# EfiPersistentMemory 0x0000000000004000&lt;BR&gt;

# OEM Reserved 0x4000000000000000&lt;BR&gt;

# OS Reserved 0x8000000000000000&lt;BR&gt;

# e.g. LoaderCode+LoaderData+BootServicesCode+BootServicesData are needed, 0x1E should be used.&lt;BR&gt;

**gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPropertyMask**

## This mask is to control Heap Guard behavior.

# Note that due to the limit of pool memory implementation and the alignment

# requirement of UEFI spec, BIT7 is a try-best setting which cannot guarantee

# that the returned pool is exactly adjacent to head guard page or tail guard

# page.

# BIT0 - Enable UEFI page guard.&lt;BR&gt;

# BIT1 - Enable UEFI pool guard.&lt;BR&gt;

# BIT2 - Enable SMM page guard.&lt;BR&gt;

# BIT3 - Enable SMM pool guard.&lt;BR&gt;

# BIT7 - The direction of Guard Page for Pool Guard.

# 0 - The returned pool is near the tail guard page.&lt;BR&gt;

# 1 - The returned pool is near the head guard page.&lt;BR&gt;

### Memory Profile: _Provide memory usage information, detect memory leak_ {#memory-profile-provide-memory-usage-information-detect-memory-leak}

**gEfiMdeModulePkgTokenSpaceGuid.PcdMemoryProfilePropertyMask**

## The mask is used to control memory profile behavior.&lt;BR&gt;&lt;BR&gt;

# BIT0 - Enable UEFI memory profile.&lt;BR&gt;

# BIT1 - Enable SMRAM profile.&lt;BR&gt;

# BIT7 - Disable recording at the start.&lt;BR&gt;

**gEfiMdeModulePkgTokenSpaceGuid.PcdMemoryProfileMemoryType**

## This flag is to control which memory types of alloc info will be recorded by DxeCore &amp; SmmCore.&lt;BR&gt;&lt;BR&gt;

# For SmmCore, only EfiRuntimeServicesCode and EfiRuntimeServicesData are valid.&lt;BR&gt;

#

# Below is bit mask for this PCD: (Order is same as UEFI spec)&lt;BR&gt;

# EfiReservedMemoryType 0x0001&lt;BR&gt;

# EfiLoaderCode 0x0002&lt;BR&gt;

# EfiLoaderData 0x0004&lt;BR&gt;

# EfiBootServicesCode 0x0008&lt;BR&gt;

# EfiBootServicesData 0x0010&lt;BR&gt;

# EfiRuntimeServicesCode 0x0020&lt;BR&gt;

# EfiRuntimeServicesData 0x0040&lt;BR&gt;

# EfiConventionalMemory 0x0080&lt;BR&gt;

# EfiUnusableMemory 0x0100&lt;BR&gt;

# EfiACPIReclaimMemory 0x0200&lt;BR&gt;

# EfiACPIMemoryNVS 0x0400&lt;BR&gt;

# EfiMemoryMappedIO 0x0800&lt;BR&gt;

# EfiMemoryMappedIOPortSpace 0x1000&lt;BR&gt;

# EfiPalCode 0x2000&lt;BR&gt;

# EfiPersistentMemory 0x4000&lt;BR&gt;

# OEM Reserved 0x4000000000000000&lt;BR&gt;

# OS Reserved 0x8000000000000000&lt;BR&gt;

#

# e.g. Reserved+ACPINvs+ACPIReclaim+RuntimeCode+RuntimeData are needed, 0x661 should be used.&lt;BR&gt;

**gEfiMdeModulePkgTokenSpaceGuid.PcdMemoryProfileDriverPath**

## This PCD is to control which drivers need memory profile data.&lt;BR&gt;&lt;BR&gt;

# For example:&lt;BR&gt;

# One image only (Shell):&lt;BR&gt;

# Header GUID&lt;BR&gt;

# {0x04, 0x06, 0x14, 0x00, 0x83, 0xA5, 0x04, 0x7C, 0x3E, 0x9E, 0x1C, 0x4F, 0xAD, 0x65, 0xE0, 0x52, 0x68, 0xD0, 0xB4, 0xD1,&lt;BR&gt;

# 0x7F, 0xFF, 0x04, 0x00}&lt;BR&gt;

# Two or more images (Shell + WinNtSimpleFileSystem):&lt;BR&gt;

# {0x04, 0x06, 0x14, 0x00, 0x83, 0xA5, 0x04, 0x7C, 0x3E, 0x9E, 0x1C, 0x4F, 0xAD, 0x65, 0xE0, 0x52, 0x68, 0xD0, 0xB4, 0xD1,&lt;BR&gt;

# 0x7F, 0x01, 0x04, 0x00,&lt;BR&gt;

# 0x04, 0x06, 0x14, 0x00, 0x8B, 0xE1, 0x25, 0x9C, 0xBA, 0x76, 0xDA, 0x43, 0xA1, 0x32, 0xDB, 0xB0, 0x99, 0x7C, 0xEF, 0xEF,&lt;BR&gt;

# 0x7F, 0xFF, 0x04, 0x00}&lt;BR&gt;

### NX stack: _Prevent code execution in stack_ {#nx-stack-prevent-code-execution-in-stack}

**gEfiMdeModulePkgTokenSpaceGuid.PcdSetNxForStack**

## Indicates if to set NX for stack.&lt;BR&gt;&lt;BR&gt;

# For the DxeIpl and the DxeCore are both X64, set NX for stack feature also require PcdDxeIplBuildPageTables be TRUE.&lt;BR&gt;

# For the DxeIpl and the DxeCore are both IA32 (PcdDxeIplSwitchToLongMode is FALSE), set NX for stack feature also require

# IA32 PAE is supported and Execute Disable Bit is available.&lt;BR&gt;

# TRUE - to set NX for stack.&lt;BR&gt;

# FALSE - Not to set NX for stack.&lt;BR&gt;

### DXE NX/RO Protection: _Prevent code injection_ {#dxe-nx-ro-protection-prevent-code-injection}

**gEfiMdeModulePkgTokenSpaceGuid.PcdDxeNxMemoryProtectionPolicy**

## Set DXE memory protection policy. The policy is bitwise.

# If a bit is set, memory regions of the associated type will be mapped

# non-executable.&lt;BR&gt;&lt;BR&gt;

#

# Below is bit mask for this PCD: (Order is same as UEFI spec)&lt;BR&gt;

# EfiReservedMemoryType 0x0001&lt;BR&gt;

# EfiLoaderCode 0x0002&lt;BR&gt;

# EfiLoaderData 0x0004&lt;BR&gt;

# EfiBootServicesCode 0x0008&lt;BR&gt;

# EfiBootServicesData 0x0010&lt;BR&gt;

# EfiRuntimeServicesCode 0x0020&lt;BR&gt;

# EfiRuntimeServicesData 0x0040&lt;BR&gt;

# EfiConventionalMemory 0x0080&lt;BR&gt;

# EfiUnusableMemory 0x0100&lt;BR&gt;

# EfiACPIReclaimMemory 0x0200&lt;BR&gt;

# EfiACPIMemoryNVS 0x0400&lt;BR&gt;

# EfiMemoryMappedIO 0x0800&lt;BR&gt;

# EfiMemoryMappedIOPortSpace 0x1000&lt;BR&gt;

# EfiPalCode 0x2000&lt;BR&gt;

# EfiPersistentMemory 0x4000&lt;BR&gt;

# OEM Reserved 0x4000000000000000&lt;BR&gt;

# OS Reserved 0x8000000000000000&lt;BR&gt;

#

# NOTE: User must NOT set NX protection for EfiLoaderCode / EfiBootServicesCode / EfiRuntimeServicesCode. &lt;BR&gt;

# User MUST set the same NX protection for EfiBootServicesData and EfiConventionalMemory. &lt;BR&gt;

#

# e.g. 0x7FD5 can be used for all memory except Code. &lt;BR&gt;

# e.g. 0x7BD4 can be used for all memory except Code and ACPINVS/Reserved. &lt;BR&gt;

### DXE image Protection: _Prevent code injection_ {#dxe-image-protection-prevent-code-injection}

**gEfiMdeModulePkgTokenSpaceGuid.PcdImageProtectionPolicy**

## Set image protection policy. The policy is bitwise.

# If a bit is set, the image will be protected by DxeCore if it is aligned.

# The code section becomes read-only, and the data section becomes non-executable.

# If a bit is clear, the image will not be protected.&lt;BR&gt;&lt;BR&gt;

# BIT0 - Image from unknown device. &lt;BR&gt;

# BIT1 - Image from firmware volume.&lt;BR&gt;

### SMM static paging: _Provide code injection in SMM_ {#smm-static-paging-provide-code-injection-in-smm}

**gUefiCpuPkgTokenSpaceGuid.PcdCpuSmmStaticPageTable**

## Indicates if SMM uses static page table.

# If enabled, SMM will not use on-demand paging. SMM will build static page table for all memory.

# This flag only impacts X64 build, because SMM always builds static page table for IA32.

# It could not be enabled at the same time with SMM profile feature (PcdCpuSmmProfileEnable).

# It could not be enabled also at the same time with heap guard feature for SMM

# (PcdHeapGuardPropertyMask in MdeModulePkg).&lt;BR&gt;&lt;BR&gt;

# TRUE - SMM uses static page table for all memory.&lt;BR&gt;

# FALSE - SMM uses static page table for below 4G memory and use on-demand paging for above 4G memory.&lt;BR&gt;

### SMI Handler Profile: _Provide SMI handler information_ {#smi-handler-profile-provide-smi-handler-information}

**gEfiMdeModulePkgTokenSpaceGuid.PcdSmiHandlerProfilePropertyMask**

## The mask is used to control SmiHandlerProfile behavior.&lt;BR&gt;&lt;BR&gt;

# BIT0 - Enable SmiHandlerProfile.&lt;BR&gt;

### SMM Profile: _Provide non-SMRAM access in SMM_ {#smm-profile-provide-non-smram-access-in-smm}

**gUefiCpuPkgTokenSpaceGuid.PcdCpuSmmProfileEnable**

## Indicates if SMM Profile will be enabled.

# If enabled, instruction executions in and data accesses to memory outside of SMRAM will be logged.

# It could not be enabled at the same time with SMM static page table feature (PcdCpuSmmStaticPageTable).

# This PCD is only for validation purpose. It should be set to false in production.&lt;BR&gt;&lt;BR&gt;

# TRUE - SMM Profile will be enabled.&lt;BR&gt;

# FALSE - SMM Profile will be disabled.&lt;BR&gt;

**gUefiCpuPkgTokenSpaceGuid.PcdCpuSmmProfileRingBuffer**

## Indicates if the SMM profile log buffer is a ring buffer.

# If disabled, no additional log can be done when the buffer is full.&lt;BR&gt;&lt;BR&gt;

# TRUE - the SMM profile log buffer is a ring buffer.&lt;BR&gt;

# FALSE - the SMM profile log buffer is a normal buffer.&lt;BR&gt;

**gUefiCpuPkgTokenSpaceGuid.PcdCpuSmmProfileSize**

## Specifies buffer size in bytes to save SMM profile data. The value should be a multiple of 4KB.