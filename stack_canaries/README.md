<!--- @file
  README.md for Stack Canaries

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
# _Stack Canaries_ {#stack-canaries}

One of the most important buffer overflow attacks is the first Internet worm, written by Robert Morris Jr. in 1988\. It modified the return address on the stack, injected malicious code, then it controlled the system. (See figure 1-1 Stack Smashing Buffer Overflow Attack)

![](/media/image1.png)
###### Figure 1-1 Stack Smashing Buffer Overflow Attack (Source: [[StackCheck](https://www.usenix.org/legacy/publications/library/proceedings/sec98/full_papers/cowan/cowan.pdf)]<sup>[[1]](#footnote1)</sup> )

In 1999, StackCheck was introduced to prevent buffer overflow attack on a stack.[[StackCheck](https://www.usenix.org/legacy/publications/library/proceedings/sec98/full_papers/cowan/cowan.pdf)]<sup>[[1]](#footnote1)</sup>> 

When the program makes a function call, it puts a random digital canary on top of the return address on the stack. When the function returns, the program checks if the canary data is modified. If it is modified, there must be something wrong and a special failure reporting function is invoked before the program returns back to the function address on the stack. (See figure 1-2 Canary Word Next to Return Address)

![](/media/image2.png)
###### Figure 1-2 Canary Word Next to Return Address (Source: [[StackCheck](https://www.usenix.org/legacy/publications/library/proceedings/sec98/full_papers/cowan/cowan.pdf)]<sup>[[1]](#footnote1)</sup>)

Stack canary is a software feature. It is supported by most compilers.

<a name="footnote1">[1]</a> [[StackCheck](https://www.usenix.org/legacy/publications/library/proceedings/sec98/full_papers/cowan/cowan.pdf)]