# _Address Space Layout Randomization_ {#address-space-layout-randomization}

Another possible way to prevent such these attacks is to provide a random address. With address space layout randomization (ASLR), the address of every function or data between every run of program is random so that it is hard for an attacker to exploit the system to know where to return.

ASLR is a software feature. It is supported by operating systems today.