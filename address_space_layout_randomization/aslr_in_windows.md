## ASLR in Windows {#aslr-in-windows}

Windows supports ASLR. [WindowsInternal] desribes the detail on how executable images, DLL, stack, heap are randomized.

![](Mydir/media/image4.png)

Figure 3-1 Windows OS space layout, source: [WindowsInternal]

[ASLR1] shows the Windows8 HE-ASLR design and entropy number.

![](Mydir/media/image5.png)

Figure 3-2 Win8 HE-ASLR, source: [ASLR1]

[ASLR2] shows different image layouts during boot.

![Diagram showing how the physical memory location of various system DLLs changes between a first and second boot.](Mydir/media/image6.png)

Figure 3-3 Image layout during boot, source: [ASLR2]