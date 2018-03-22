## Future work {#future-work}

Both software and hardware-based advances can be added to strengthen code against this class of issue. On the software front, language-based security may offer some relief. This can span using a safer variant of C [CHECKED__C] to refactoring code to a type-safe language [RUST]. These are huge tasks, though, given the existing software catalog and would challenge software portability. As such, a language-based approach is not a near term option.

As we go from software to hardware, though, one option appears feasible. Specifically, recent hardware advances include the Intel® Memory Protection Extensions (Intel® MPX). This is a new capability introduced into Intel Architecture [IA32SDM][MPX]. Intel MPX can help detect the buffer overflow or underflow with a set of new MPX instructions and the compiler support. When MPX is enabled, a Bounds Table is constructed to store the pointer value, lower bound of the buffer, and the upper bound of the buffer. See figure 4-12.

The BNDMK instruction can create LowerBound (LB) and UpperBound (UB) in bounds register. The BNDCL/BNDCU/BNDCN instruction can check the address of a memory reference or address against the LB or UB. A BOUND Range Exceeded exception (#BR) is raised if any of the bounds compare instructions fail.

Intel MPX need compiler support. MSVC 2015 Update 1 and GCC 5.1 supports Intel MPX.

![](Mydir/media/image27.png)

Figure 4-12 Bound Table, (source: [MPX])

Intel MPX may also be considered to add to a UEFI firmware to help catch the heap pool overflow or the global variable overflow.

### Summary {#summary}

This section discussed some other mechanism which can be used to detect stack overflow or heap overflow in EDKII.