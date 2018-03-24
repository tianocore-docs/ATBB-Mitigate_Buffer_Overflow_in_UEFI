<!--- @file
 Address Space Layout Randomization file: ASLR in Windows

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
## Address Sace Layout Randomization (ASLR) in Windows\* {#aslr-in-windows}

Windows supports Address Sace Layout Randomization (ASLR). [[WindowsInternal](https://www.amazon.com/Windows-Internals-Part-Developer-Reference/dp/0735648735 )] <sup>[[1]](#footnote1)</sup>  desribes the detail on how executable images, DLL, stack, heap are randomized.

![](/media/image4.png)

###### Figure 3-1 Windows OS space layout, source: [[WindowsInternal](https://www.amazon.com/Windows-Internals-Part-Developer-Reference/dp/0735648735 )] <sup>[[1]](#footnote1)</sup>

[[ASLR1](http://media.blackhat.com/bh-us-12/Briefings/M_Miller/BH_US_12_Miller_Exploit_Mitigation_Slides.pdf)]<sup>[[2]](#footnote2)</sup> shows the Windows8 HE-ASLR design and entropy number.

![](/media/image5.png)

###### Figure 3-2 Win8 HE-ASLR, source: [[ASLR1](http://media.blackhat.com/bh-us-12/Briefings/M_Miller/BH_US_12_Miller_Exploit_Mitigation_Slides.pdf)]<sup>[[2]](#footnote2)</sup>

[[ASLR2](http://blogs.msdn.com/b/ie/archive/2012/03/12/enhanced-memory-protections-in-ie10.aspx)]<sup>[[3]](#footnote3)</sup> shows different image layouts during boot.

The following Diagram showing how the physical memory location of various system DLLs changes between a first and second boot

![](/media/image6.png)

###### Figure 3-3 Image layout during boot, source: [[ASLR2](http://blogs.msdn.com/b/ie/archive/2012/03/12/enhanced-memory-protections-in-ie10.aspx)]<sup>[[3]](#footnote3)</sup>

<BR>
<BR>
<BR>
<hr>






<a name="footnote1">[1]</a> [[WindowsInternal](https://www.amazon.com/Windows-Internals-Part-Developer-Reference/dp/0735648735 )] Windows Internals, 6th edition, Mark E. Russinovich, David A. Solomon, Alex Ionescu, 2012, Microsoft Press. ISBN-13: 978-0735648739/978-0735665873

<a name="footnote2">[2]</a>[[ASLR1](http://media.blackhat.com/bh-us-12/Briefings/M_Miller/BH_US_12_Miller_Exploit_Mitigation_Slides.pdf)] Exploit Mitigation Improvements in Windows 8, Ken Johnson, Ma, Miller

<a name="footnote3">[3]</a>[[ASLR2](http://blogs.msdn.com/b/ie/archive/2012/03/12/enhanced-memory-protections-in-ie10.aspx)] Enhance Memory Protections in IE10

