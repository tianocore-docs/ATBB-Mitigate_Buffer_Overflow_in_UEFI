<!--- @file
  README.md for Stack Canaries - Stack Check Support in Microsoft Visual Studio 

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

## Stack Check Support in Microsoft Visual Studio {#stack-check-support-in-microsoft-visual-studio}

Microsoft Visual Studio supports a stack guard function. “Compiler Security Checks In Depth” [[MSVC](https://msdn.microsoft.com/library/aa290051.aspx)] <sup>[[1]](#footnote1)</sup>
introduces the detail on how it works. There are 2 compiler options related: /GS and /RTCs.

`/GS `[[MSVC_GS](/ https://msdn.microsoft.com/en-us/library/8dbf701c.aspx)] <sup>[[2]](#footnote2)</sup>   is designed to detect some buffer overruns that overwrite a function&#039;s return address. It is similar to the stack guard feature described above.

`/RTCs`[[MSVC_RTC](https://msdn.microsoft.com/en-US/library/8wtf2dfz.aspx)] <sup>[[3]](#footnote2)</sup>   is designed to put 2 tags around (before and after) all individual buffers allocated on the stack. Therefore, both overruns and underflows can be caught.

See figure 1-3 Microsoft Stack Check.

![](/media/image3.png)

###### Figure 1-3 – Microsoft Stack Check

<BR>
<BR>
<BR>
<hr>


<a name="footnote1">[1]</a> [[MSVC](https://msdn.microsoft.com/library/aa290051.aspx)] Compiler Security Checks In Depth

<a name="footnote2">[2]</a> [[MSVC_GS](/ https://msdn.microsoft.com/en-us/library/8dbf701c.aspx)] /GS (Buffer Security Check)

<a name="footnote3">[3]</a> [[MSVC_RTC](https://msdn.microsoft.com/en-US/library/8wtf2dfz.aspx)]  /RTC (Run-Time Error Checks) 

