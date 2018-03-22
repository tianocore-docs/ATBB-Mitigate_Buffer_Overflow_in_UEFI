## Enable Stack Check in EDKII {#enable-stack-check-in-edkii}

Current EDKII uses /GS- for MSVC and -fno-stack-protector for GCC. The stack check feature is disabled by default. The reason is that EDKII does not link against any compiler provided libraries. If /GS or -fstack-protector is enabled, the link will fail due to no symbol detected for __security_cookie/ __security_check_cookie() or __stack_chk_guard/__stack_chk_fail().

In order to enable a stack check, we provide an implementation for the above symbols at [https://github.com/jyao1/SecurityEx/tree/master/StackCheckPkg/Library/StackCheckLib](https://github.com/jyao1/SecurityEx/tree/master/StackCheckPkg/Library/StackCheckLib).

As such, any drivers or applications can use /GS or -fstack-protector-strong to prevent the stack smash attack. The sample driver [https://github.com/jyao1/SecurityEx/tree/master/StackCheckPkg/Test/StackCookieTest](https://github.com/jyao1/SecurityEx/tree/master/StackCheckPkg/Test/StackCookieTest) shows how stack check works in UEFI.