<!--- @file
  References File: -Stack Canaries

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

## Stack Canaries {#stack-canaries}

[StackCanaries] [http://en.wikipedia.org/wiki/Buffer_overflow_protection](http://en.wikipedia.org/wiki/Buffer_overflow_protection)

[StackCheck] _StackGuard: Automatic Adaptive Detection and Prevention of Buffer-Overflow Attacks._ Cowan, C., Pu, C., Maier, D., Hintongif, H., Walpole, J., Bakke, P., Beattie, S., Grier, A., Wagle, P., Zhang, Q. Proceedings of the 7th USENIX Security Symposium (January 1998), [https://www.usenix.org/legacy/publications/library/proceedings/sec98/full_papers/cowan/cowan.pdf](https://www.usenix.org/legacy/publications/library/proceedings/sec98/full_papers/cowan/cowan.pdf)

[MSVC] _Compiler Security Checks In Depth_, [https://msdn.microsoft.com/library/aa290051.aspx](https://msdn.microsoft.com/library/aa290051.aspx)

[MSVC_GS] _/GS (Buffer Security Check)_, [https://msdn.microsoft.com/en-us/library/8dbf701c.aspx](https://msdn.microsoft.com/en-us/library/8dbf701c.aspx)

[MSVC_RTC] _/RTC (Run-Time Error Checks)_, [https://msdn.microsoft.com/en-US/library/8wtf2dfz.aspx](https://msdn.microsoft.com/en-US/library/8wtf2dfz.aspx)

[MSVC_FASTFAIL] __fastfail_, [https://msdn.microsoft.com/en-us/library/dn774154.aspx](https://msdn.microsoft.com/en-us/library/dn774154.aspx)

[GCC] _Proposal to add a new stack-smashing-attack protection mechanism “-fstack-protector-strong”_, [https://docs.google.com/document/d/1xXBH6rRZue4f296vGt9YQcuLVQHeE516stHwt8M9xyU/edit](https://docs.google.com/document/d/1xXBH6rRZue4f296vGt9YQcuLVQHeE516stHwt8M9xyU/edit)

[PI] UEFI Platform Initialization Specification, Version 1.5 [http://www.uefi.org/sites/default/files/resources/PI%201.5.zip](http://www.uefi.org/sites/default/files/resources/PI%201.5.zip)