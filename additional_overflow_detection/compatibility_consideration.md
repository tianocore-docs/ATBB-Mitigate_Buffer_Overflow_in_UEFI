<!--- @file
  Additional Overflow Detection file: -Compatibility Consideration

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

## Compatibility Consideration {#compatibility-consideration}

1.  OS compatibility

    If the heap guard is enabled (especially pool guard), the UEFI memory map is fragmented. We notice that the fragmentation may cause OS boot or installation fail. For example, Windows Boot Manager sets the maximum number of global memory descriptor for a 64-bit UEFI system at 512\. ([https://support.microsoft.com/en-us/help/4020050/blinitializelibrary-failed-xxx-error-when-you-install-or-start-an-oper](https://support.microsoft.com/en-us/help/4020050/blinitializelibrary-failed-xxx-error-when-you-install-or-start-an-oper))

    For NULL pointer detection, BIT7 of PcdNullPointerDetectionPropertyMask (disables NULL pointer detection just after EndOfDxe) is a workaround for those unsolvable NULL access issues in Option ROM, OS boot loader, such as Windows 7 boot on Qemu.

2.  3rd part driver (PCI Option ROM)

    When the heap guard is enabled, we observed the #PF (Page Fault) exception happens and the instruction address is within a 3<sup>rd</sup> part PCI Option ROM.

3.  Legacy CSM

    The legacy CSM module may need access the zero address and the first 4KiB memory, such as IVT (Interrupt Vector Table) and BDS (BIOS Data Area). Whenever the legacy module accesses the first 4KiB memory, the code must be included by ACCESS_PAGE0_CODE() macro. ([https://github.com/tianocore/edk2/blob/master/IntelFrameworkPkg/Include/Protocol/LegacyBios.h](https://github.com/tianocore/edk2/blob/master/IntelFrameworkPkg/Include/Protocol/LegacyBios.h)). For example, when the LegacyBios driver accesses IVT region ([https://github.com/tianocore/edk2/blob/master/IntelFrameworkModulePkg/Csm/LegacyBiosDxe/Thunk.c](https://github.com/tianocore/edk2/blob/master/IntelFrameworkModulePkg/Csm/LegacyBiosDxe/Thunk.c)) or when the LegacyKeyboard driver accesses BDS region ([https://github.com/tianocore/edk2/blob/master/IntelFrameworkModulePkg/Csm/BiosThunk/KeyboardDxe/BiosKeyboard.c](https://github.com/tianocore/edk2/blob/master/IntelFrameworkModulePkg/Csm/BiosThunk/KeyboardDxe/BiosKeyboard.c)).

    The platform specific LegacyBiosPlatform driver also need update to add ACCESS_PAGE0_CODE() macro around the code to update IVT or BDA.

4.  CPU driver

    The EDKII DxeCore relies on CPU driver EFI_CPU_ARCH_PROTOCOL.SetMemoryAttributes ([https://github.com/tianocore/edk2/blob/master/MdePkg/Include/Protocol/Cpu.h](https://github.com/tianocore/edk2/blob/master/MdePkg/Include/Protocol/Cpu.h)) to update the page table ([https://github.com/tianocore/edk2/blob/master/UefiCpuPkg/CpuDxe/CpuPageTable.c](https://github.com/tianocore/edk2/blob/master/UefiCpuPkg/CpuDxe/CpuPageTable.c)). The EDKII PiSmmCore also relies on PiSmmCpu driver EDKII_SMM_MEMORY_ATTRIBUTE_PROTOCOL ([https://github.com/tianocore/edk2/blob/master/MdeModulePkg/Include/Protocol/SmmMemoryAttribute.h](https://github.com/tianocore/edk2/blob/master/MdeModulePkg/Include/Protocol/SmmMemoryAttribute.h))to update the page table ([https://github.com/tianocore/edk2/blob/master/UefiCpuPkg/PiSmmCpuDxeSmm/SmmCpuMemoryManagement.c](https://github.com/tianocore/edk2/blob/master/UefiCpuPkg/PiSmmCpuDxeSmm/SmmCpuMemoryManagement.c)). If a platform uses its own CPU driver instead of the open source one, this platform need add the page table update capability in the CPU driver.