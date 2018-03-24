<!--- @file
  README.md for Data Execution Protection

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
# _Data Execution Protection_ {#data-execution-protection}

Stack smash attacks may inject code. The other possible way to prevent such an attack is to prevent malicious code from executing. Some modern OS’s already have Data Execution Protection (DEP) support [[DEP](http://media.blackhat.com/bh-us-12/Briefings/M_Miller/BH_US_12_Miller_Exploit_Mitigation_Slides.pdf )] <sup>[[1]](#footnote1)</sup> [[PaX](/ https://pax.grsecurity.net/)] <sup>[[2]](#footnote2)</sup>. DEP may be applied to: [[WindowsInternal](https://www.amazon.com/Windows-Internals-Part-Developer-Reference/dp/0735648735 )]<sup>[[3]](#footnote3)</sup>  

*   User mode stacks
*   User mode pages not specifically marked as executable
*   Kernel mode Stacks
*   kernel paged pool (X64)
*   kernel session pool (X64)

Research shows 14 of 19 exploits from popular exploit kits fail with DEP enabled. [[DEP](http://media.blackhat.com/bh-us-12/Briefings/M_Miller/BH_US_12_Miller_Exploit_Mitigation_Slides.pdf )] <sup>[[1]](#footnote1)</sup>.

<BR>
<BR>
<BR>
<hr>





<a name="footnote1">[1]</a>[[DEP](http://media.blackhat.com/bh-us-12/Briefings/M_Miller/BH_US_12_Miller_Exploit_Mitigation_Slides.pdf )] Exploit Mitigation Improvements in Windows 8, Ken Johnson, Ma, Miller

<a name="footnote2">[2]</a>[[PaX](/ https://pax.grsecurity.net/)] PaX Home Page, https://pax.grsecurity.net/

<a name="footnote3">[3]</a>[[WindowsInternal](https://www.amazon.com/Windows-Internals-Part-Developer-Reference/dp/0735648735 )] Windows Internals, 6th edition, Mark E. Russinovich, David A. Solomon, Alex Ionescu, 2012, Microsoft Press. ISBN-13: 978-0735648739/978-0735665873


