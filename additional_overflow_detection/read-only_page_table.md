## Read-only page table {#read-only-page-table}

Because we use CPU page table to provide such detection, DxeIpl does one more enhancement to set page table itself to be read only. ([https://github.com/tianocore/edk2/blob/master/MdeModulePkg/Core/DxeIplPeim/X64/VirtualMemory.c](https://github.com/tianocore/edk2/blob/master/MdeModulePkg/Core/DxeIplPeim/X64/VirtualMemory.c) SetPageTablePoolReadOnly()) If the buffer overflow impacts the page table, it can be detected immediately.

The CPU driver need be aware of this and carefully clear CR0_WP bit before modifying the page table and restore CR0 after modification. ([https://github.com/tianocore/edk2/blob/master/UefiCpuPkg/CpuDxe/CpuPageTable.c](https://github.com/tianocore/edk2/blob/master/UefiCpuPkg/CpuDxe/CpuPageTable.c))