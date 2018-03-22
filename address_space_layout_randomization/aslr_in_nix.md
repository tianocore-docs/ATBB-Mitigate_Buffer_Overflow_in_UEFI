<!--- @file
 Address Space Layout Randomization file: ASLR in *nix

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
## Address Sace Layout Randomization (ASLR) in *nix {#aslr-in-nix}

[[PaX](https://grsecurity.net/PaX-presentation.ppt)] <sup>[[1]](#footnote1)</sup>  also provides an ASLR patch for Linux and OpenBSD. [[OpenBSD](http://www.openbsd.org/papers/ven05-deraadt)]<sup>[[2]](#footnote2)</sup>  and [[PIE](http://www.openbsd.org/papers/nycbsdcon08-pie/)]<sup>[[3]](#footnote3)</sup>  provide detailed information on the randomized image layout.

<hr>


<a name="footnote1">[1]</a> [[PaX](https://grsecurity.net/PaX-presentation.ppt)] PaX presentation, Brad Spengler,

<a name="footnote2">[2]</a>[[OpenBSD](http://www.openbsd.org/papers/ven05-deraadt)] Exploit Mitigation Techniques, Theo de Raadt

<a name="footnote3">[3]</a>[[PIE](http://www.openbsd.org/papers/nycbsdcon08-pie/)] OpenBSD’s Position Independent Executable (PIE) Implementation, Kurt Miller, 
