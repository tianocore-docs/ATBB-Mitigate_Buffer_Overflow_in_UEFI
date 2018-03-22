<!--- @file
 Address Space Layout Randomization file: ASLR requirement in UEFI firmware

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
## Address Sace Layout Randomization (ASLR) requirement in UEFI firmware {#aslr-requirement-in-uefi-firmware}

The current EDK II code does not support address space randomization. The memory allocation algorithm is top-down. In order to support the randomization in the pre-boot environment, we define below requirement:

1.  **The randomization algorithm should keep UEFI firmware boot behavior consistent**. If a system has enough memory for boot, it should be able to boot at any time. If a system is out of memory, it should be out of memory for any boot. If a UEFI firmware boots at some time because the memory is enough, but it may fail at some other time because the randomization cause memory being exhausted, then it is not acceptable solution. This is very important for a resource constrained environment, such as System Management Mode (SMM)  or the Pre-EFI Initialization (PEI) phase.

2.  **The randomization algorithm should keep OS resume from sleep states required memory being consistent**. An OS may needs to support S4 or S3 resume feature. The OS resume may have some assumption that some special memory is unchanged, such as the runtime memory, or the ACPI memory.

3.  **Any individual component may have its own randomization algorithm.** For example, the Global Descriptor Table (GDT), Interrupt Descriptor Table (IDT), or Page Table are allocated from heap memory. Even if the heap has randomized, the CPU driver can have additional randomization for GDT/IDT/PageTable specifically.