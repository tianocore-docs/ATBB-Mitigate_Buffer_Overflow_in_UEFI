## Future work {#future-work}

The current stack error handler just uses CpuDeadLoop(). It is enough in preboot phase, but it is a bad idea in OS runtime. If a UEFI runtime module enables stack check, we need figure out a better way to signal the error to operating system. For example, we can use __fastfail to notify OS kernel. “The **__fastfail** intrinsic provides a mechanism for a _fast fail_ request—a way for a potentially corrupted process to request immediate process termination.” [MSVC_FASTFAIL]

If a SMM module enables stack check, the fail program cannot use __fastfail directly. It can choose deadloop, reset system, or inject System Control Interrupt (SCI) and do a long jump to a known good point to finish resource cleanup and execute RSM instruction to return to OS, then fail in OS eventually. From a software engineering standpoint, the UEFI Platform Initialization [PI] Specification defines a ReportStatusCode service for SMM, generalized to “MM” for SMM and TrustZone, and DXE, which extends into UEFI runtime. Exception handling code can invoke ReportStatusCode so that a platform can provide market or product-specific behavior, including a while (1) loop that pulses an LED for a closed box client, all the way up to a multi-socket server that might record the result of the failure in a baseboard management controller (BMC).

### Summary {#summary}

This section introduces the concept of stack canaries and how to enable this feature in EDKII.