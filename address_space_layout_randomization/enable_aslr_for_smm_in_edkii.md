<!--- @file
 Address Space Layout Randomization file: Enable ASLR for SMM in EDKII

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
## Enable Enable Address Sace Layout Randomization (ASLR) for System Mamangement Mode (SMM) in EDK II {#enable-aslr-for-smm-in-edkii}

System Management Mode (SMM) is a resource constrained environment.

*   **SmmCore randomization**.

The `SmmCore` is loaded by `SmmIpl`, and `SmmIpl` need find all SMRAM and allocate the top of SMRAM for `SmmCore`. `ExecuteSmmCoreFromSmram()` ([https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/Override/MdeModulePkg/Core/PiSmmCore/PiSmmIpl.c](https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/Override/MdeModulePkg/Core/PiSmmCore/PiSmmIpl.c)) allocates the SMRAM for `SmmCore`, plus the maximum pages needed by randomization. Then it shifts the `SmmCore` inside of the whole allocated memory. This is designed to meet the requirement 1 – to make sure the SMRAM consumption is consistent.

*   **SMM heap randomization**.
The SMM heap randomization is handled in [https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/Override/MdeModulePkg/Core/PiSmmCore/Page.c](https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/Override/MdeModulePkg/Core/PiSmmCore/Page.c). When a new SMRAM block is found, the `SmmAddMemoryRegion()` function reserves the some fixed length pages and shift the valid SMRAM inside of whole SMRAM. 
The same design philosophy can be adopted by any randomization in SMM, such as stack, page table, GDT, IDT, etc. The key is to allocate MAX fixed length pages, and shift content inside of it, in order to ensure that the SMRAM consumption is consistent in every boot.

Figure 3-7 shows the SMM memory layout.

![](/media/image10.png)

###### Figure 3-7 SMM memory layout

*   **SMM image randomization.**
SMM image randomization is similar to UEFI image randomization. When `PcdImageShuffleEnable` is TRUE, the `SmmCore` dispatcher function `SmmDriverDispatchHandler()` ([https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/Override/MdeModulePkg/Core/PiSmmCore/Dispatcher.c](https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/Override/MdeModulePkg/Core/PiSmmCore/Dispatcher.c)) calls `SmmCoreLoadImages()` to load all images with shuffled order before the dependency section is evaluated as we discussed above.
Just as for UEFI, the SMM image shuffle only controls *image load*. It does not control *image start*. The image start process is unchanged. `SmmCore` only starts an image after its dependency is satisfied.

*   **SMM information leak prevention.**
SMM is considered as an isolated and secure execution environment. We randomize the component in SMM to prevent attacks. However, if the randomized information is exposed, it is considered as an information leak.
In the current EDK II, the SmmCore installs an `EFI_LOADED_IMAGE_PROTOCOL` into DXE protocol database for each SMM images. This `EFI_LOADED_IMAGE_PROTOCOL` contains the SMM image base and size information. This is a typical SMM information leak and make SMM image randomization useless.

In order to mitigate this, `SmmLoadImage()` ([https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/Override/MdeModulePkg/Core/PiSmmCore/Dispatcher.c](https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/Override/MdeModulePkg/Core/PiSmmCore/Dispatcher.c)) installs the `EFI_LOADED_IMAGE_PROTOCOL` into SMM protocol database to make SMM information self-contained.

