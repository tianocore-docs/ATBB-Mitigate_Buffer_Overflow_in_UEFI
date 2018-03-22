<!--- @file
   Stack Canaries - Enable Stack Check in EDK II

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

## Enable Stack Check in EDK II {#enable-stack-check-in-edkii}

Current EDK II uses /GS- for MSVC and -fno-stack-protector for GCC. The stack check feature is disabled by default. The reason is that EDKII does not link against any compiler provided libraries. If /GS or -fstack-protector is enabled, the link will fail due to no symbol detected for __security_cookie/ __security_check_cookie() or __stack_chk_guard/__stack_chk_fail().

In order to enable a stack check, we provide an implementation for the above symbols at [https://github.com/jyao1/SecurityEx/tree/master/StackCheckPkg/Library/StackCheckLib](https://github.com/jyao1/SecurityEx/tree/master/StackCheckPkg/Library/StackCheckLib).

As such, any drivers or applications can use /GS or -fstack-protector-strong to prevent the stack smash attack. The sample driver [https://github.com/jyao1/SecurityEx/tree/master/StackCheckPkg/Test/StackCookieTest](https://github.com/jyao1/SecurityEx/tree/master/StackCheckPkg/Test/StackCookieTest) shows how stack check works in UEFI.