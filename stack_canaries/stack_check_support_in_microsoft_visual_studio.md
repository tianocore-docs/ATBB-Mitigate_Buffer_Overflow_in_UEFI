## Stack Check Support in Microsoft Visual Studio {#stack-check-support-in-microsoft-visual-studio}

Microsoft Visual Studio supports a stack guard function. “Compiler Security Checks In Depth” [MSVC] introduces the detail on how it works. There are 2 compiler options related: /GS and /RTCs.

/GS [MSVC_GS] is designed to detect some buffer overruns that overwrite a function&#039;s return address. It is similar to the stack guard feature described above.

/RTCs [MSVC_RTC] is designed to put 2 tags around (before and after) all individual buffers allocated on the stack. Therefore, both overruns and underflows can be caught.

See figure 1-3 Microsoft Stack Check.

![](Mydir/media/image3.png)

Figure 1-3 – Microsoft Stack Check