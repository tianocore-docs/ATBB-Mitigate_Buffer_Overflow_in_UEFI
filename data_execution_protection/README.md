# _Data Execution Protection_ {#data-execution-protection}

Stack smash attacks may inject code. The other possible way to prevent such an attack is to prevent malicious code from executing. Some modern OS’s already have Data Execution Protection (DEP) support [DEP][PaX]. DEP may be applied to: [WindowsInternal]

*   User mode stacks

*   User mode pages not specifically marked as executable

*   Kernel mode Stacks

*   kernel paged pool (X64)

*   kernel session pool (X64)

Research shows 14 of 19 exploits from popular exploit kits fail with DEP enabled. [DEP].