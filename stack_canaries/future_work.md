<!--- @file
  README.md for Stack Canaries - Future work

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

The current stack error handler just uses CpuDeadLoop(). It is enough in preboot phase, but it is a bad idea in OS runtime. If a UEFI runtime module enables stack check, we need figure out a better way to signal the error to operating system. For example, we can use __fastfail to notify OS kernel. “The **__fastfail** intrinsic provides a mechanism for a _fast fail_ request—a way for a potentially corrupted process to request immediate process termination.” [MSVC_FASTFAIL]

If a SMM module enables stack check, the fail program cannot use __fastfail directly. It can choose deadloop, reset system, or inject System Control Interrupt (SCI) and do a long jump to a known good point to finish resource cleanup and execute RSM instruction to return to OS, then fail in OS eventually. From a software engineering standpoint, the UEFI Platform Initialization [PI] Specification defines a ReportStatusCode service for SMM, generalized to “MM” for SMM and TrustZone, and DXE, which extends into UEFI runtime. Exception handling code can invoke ReportStatusCode so that a platform can provide market or product-specific behavior, including a while (1) loop that pulses an LED for a closed box client, all the way up to a multi-socket server that might record the result of the failure in a baseboard management controller (BMC).

### Summary {#summary}

This section introduces the concept of stack canaries and how to enable this feature in EDKII.