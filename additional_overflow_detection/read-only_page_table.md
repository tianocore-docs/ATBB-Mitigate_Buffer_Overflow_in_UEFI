<!--- @file
  Additional Overflow Detection file: -Read-only page table

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

## Read-only page table {#read-only-page-table}

Because we use CPU page table to provide such detection, `DxeIpl` does one more enhancement to set page table itself to be read only. ([https://github.com/tianocore/edk2/blob/master/MdeModulePkg/Core/DxeIplPeim/X64/VirtualMemory.c](https://github.com/tianocore/edk2/blob/master/MdeModulePkg/Core/DxeIplPeim/X64/VirtualMemory.c) `SetPageTablePoolReadOnly()`) If the buffer overflow impacts the page table, it can be detected immediately.

The CPU driver needs to be aware of this and carefully clear `CR0_WP` bit before modifying the page table and restore `CR0` after modification. ([https://github.com/tianocore/edk2/blob/master/UefiCpuPkg/CpuDxe/CpuPageTable.c](https://github.com/tianocore/edk2/blob/master/UefiCpuPkg/CpuDxe/CpuPageTable.c))