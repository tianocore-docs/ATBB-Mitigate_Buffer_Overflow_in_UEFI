<!--- @file
  Additional Overflow Detection file: -Future work

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

## Future work {#future-work}

Both software and hardware-based advances can be added to strengthen code against this class of issue. On the software front, language-based security may offer some relief. This can span using a safer variant of C [CHECKED__C] to refactoring code to a type-safe language [RUST]. These are huge tasks, though, given the existing software catalog and would challenge software portability. As such, a language-based approach is not a near term option.

As we go from software to hardware, though, one option appears feasible. Specifically, recent hardware advances include the Intel® Memory Protection Extensions (Intel® MPX). This is a new capability introduced into Intel Architecture [IA32SDM][MPX]. Intel MPX can help detect the buffer overflow or underflow with a set of new MPX instructions and the compiler support. When MPX is enabled, a Bounds Table is constructed to store the pointer value, lower bound of the buffer, and the upper bound of the buffer. See figure 4-12.

The BNDMK instruction can create LowerBound (LB) and UpperBound (UB) in bounds register. The BNDCL/BNDCU/BNDCN instruction can check the address of a memory reference or address against the LB or UB. A BOUND Range Exceeded exception (#BR) is raised if any of the bounds compare instructions fail.

Intel MPX need compiler support. MSVC 2015 Update 1 and GCC 5.1 supports Intel MPX.

![](Mydir/media/image27.png)

Figure 4-12 Bound Table, (source: [MPX])

Intel MPX may also be considered to add to a UEFI firmware to help catch the heap pool overflow or the global variable overflow.

### Summary {#summary}

This section discussed some other mechanism which can be used to detect stack overflow or heap overflow in EDK II.