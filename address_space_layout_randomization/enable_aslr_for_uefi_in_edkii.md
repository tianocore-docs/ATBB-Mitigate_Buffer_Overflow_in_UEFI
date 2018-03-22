## Enable ASLR for UEFI in EDKII {#enable-aslr-for-uefi-in-edkii}

In order to enable address space layout randomization, we provide a sample implementation for randomization in UEFI.

*   **Randomization control**.

    The gEfiAslrPkgTokenSpaceGuid.PcdASLRMinimumEntropyBits ([https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/AslrPkg.dec](https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/AslrPkg.dec)) to indicate the ASLR entropy bits. 0 means no randomization.

    The entropy bit controls the how much randomness we want to achieve.

*   **UEFI stack randomization**.

    The stack for DxeCore is allocated in HandOffToDxeCore() [https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/Override/MdeModulePkg/Core/DxeIplPeim/DxeLoad.c](https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/Override/MdeModulePkg/Core/DxeIplPeim/DxeLoad.c). Before the DXE stack is allocated from heap in the PEI phase, AllocateRandomPages() is called to allocate some random pages to shift the PEI heap.

*   **DxeCore randomization**.

    The DxeCore is also loaded from PEI heap by DxeIplFindDxeCore() [https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/Override/MdeModulePkg/Core/DxeIplPeim/DxeLoad.c](https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/Override/MdeModulePkg/Core/DxeIplPeim/DxeLoad.c). AllocateRandomPages() also helps shift the DxeCore memory.

*   **UEFI heap randomization**.

    The heap for DxeCore is reported by PEI and discovered by DxeCore in [https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/Override/MdeModulePkg/Core/Dxe/Gcd/Gcd.c](https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/Override/MdeModulePkg/Core/Dxe/Gcd/Gcd.c). After CoreInitializeMemoryServices() adds available memory to UEFI heap, AllocateRandomPages() is called to allocate some random pages to shift the UEFI heap.

    NOTE: The OS aware memory, such as runtime, ACPI, and reserved memory are pre-reserved in PEI phase. They are not impacted by the UEFI heap randomization.

    The final memory layout in UEFI is shown in figure 3-4.

    ![](Mydir/media/image7.png)

    Figure 3-4 UEFI memory layout

*   **UEFI image randomization**.

    The UEFI randomized heap shifts are implemented with a fixed offset. As such, even memory allocation shifts occur with the fixed offset. It is not good enough for a PE/COFF image load.

    For PE/COFF images we use “image shuffle” to randomize the image load order. Whenever the DxeCore discovers a new firmware volume (FV), the DxeCore unconditionally load all the images in this FV with a random order. See figure 3-5 Image shuffle.

![](Mydir/media/image8.png)

Figure 3-5 Image Shuffle

For example, if an FV contains 4 images – A, B, C, D. The loaded image order in memory is different among the 1<sup>st</sup> boot, the 2<sup>nd</sup> boot, and the 3<sup>rd</sup> boot.

Now let’s see how the Core shuffles images.

The DxeCore maintains the image information in below data structure:

![](Mydir/media/image9.png)

Figure 3-6 Core Image Database

mDiscoveredList is a linked list for all discovered images in the firmware volume. mScheduledQueue is a subset of mDiscoveredList and mScheduledQueue records the linked list of the image whose dependency is satisfied and ready to run.

The pseudo code for current core dispatch is below:

==============================

Scan FV, put to DiscoveredList.

Check Apriori, put to Scheduled List.

While (TRUE) {

For image in ScheduledList {

LoadImage()

call entrypoint // StartImage()

}

Check dependency, put to Scheduled List.

}

==============================

With ASLR capability, the core dispatch logic is updated to below:

==============================

Scan FV, put to DiscoveredList.

For image in DiscoveredList {

Copy Information to local cache

}

Shuffle image order in local cache

For image in local cache {

LoadImage()

}

Check Apriori, put to Scheduled List.

While (TRUE) {

For image in ScheduledList {

call entrypoint // StartImage()

}

Check dependency, put to Scheduled List.

}

==============================

The RED part is the additional step to implement the image shuffle. The LoadImage() is moved earlier.

The image shuffle capability is controlled by gEfiAslrPkgTokenSpaceGuid.PcdImageShuffleEnable ([https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/AslrPkg.dec](https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/AslrPkg.dec)).

When this PCD is TRUE, the DxeCore dispatcher function CoreFwVolEventProtocolNotify() ([https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/Override/MdeModulePkg/Core/Dxe/Dispatcher/Dispatcher.c](https://github.com/jyao1/SecurityEx/blob/master/AslrPkg/Override/MdeModulePkg/Core/Dxe/Dispatcher/Dispatcher.c)) calls DxeCoreLoadImages() to load all images with shuffled order before the dependency section is evaluated, as we discussed above.

Image shuffle just controls *image load*, it does not control *image start*. The image start process is unchanged. DxeCore only starts an image after its dependency is satisfied.