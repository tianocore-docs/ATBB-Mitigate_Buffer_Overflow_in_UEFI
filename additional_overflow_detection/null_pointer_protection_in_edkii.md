<!--- @file
  Additional Overflow Detection file: -NULL Pointer Protection in EDKII

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

## NULL Pointer Protection in EDKII {#null-pointer-protection-in-edkii}

Zero address is considered as an invalid address in most programs. However, in x86 systems, the zero address is valid address in legacy BIOS because the 16bit interrupt vector table (IVT) is at address zero. In current UEFI firmware, zero address is always mapped.

We can do some enhancement here. Once the 16bit legacy support is dropped in UEFI firmware, it is possible to mark the first 4K page at address zero to be invalid for X86 system. Then, we can catch the zero address reference if a program does not check memory allocation successful or not.

Since CSM/legacy boot needs to be disabled for OS compliance when using UEFI Secure Boot, few systems are seen in the market requiring this memory to be mapped at zero.

We define a gEfiMdeModulePkgTokenSpaceGuid.PcdNullPointerDetectionPropertyMask ([https://github.com/tianocore/edk2/blob/master/MdeModulePkg/MdeModulePkg.dec](https://github.com/tianocore/edk2/blob/master/MdeModulePkg/MdeModulePkg.dec)). If the BIT0 of PcdNullPointerDetectionPropertyMask is set, the [https://github.com/tianocore/edk2/tree/master/MdeModulePkg/Core/DxeIplPeim](https://github.com/tianocore/edk2/tree/master/MdeModulePkg/Core/DxeIplPeim) clears the PRESENT bit of the address zero page. As such, a Page Fault exception will be generated if some program access to address zero. The BIT1 of PcdNullPointerDetectionPropertyMask controls the NULL pointer detection in SMM environment, it is referred by [https://github.com/tianocore/edk2/tree/master/UefiCpuPkg/PiSmmCpuDxeSmm](https://github.com/tianocore/edk2/tree/master/UefiCpuPkg/PiSmmCpuDxeSmm). The BIT7 of PcdNullPointerDetectionPropertyMask disables NULL pointer detection just after EndOfDxe. This is a workaround for those unsolvable NULL access issues in OptionROM, boot loader, etc. It can also help to avoid unnecessary exception caused by legacy memory (0-4095) access after EndOfDxe, such as Windows 7 boot on Qemu. BIT7 is checked by [https://github.com/tianocore/edk2/tree/master/MdeModulePkg/Core/Dxe](https://github.com/tianocore/edk2/tree/master/MdeModulePkg/Core/Dxe).