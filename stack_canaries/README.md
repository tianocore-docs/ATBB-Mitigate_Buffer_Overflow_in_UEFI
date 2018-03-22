# _Stack Canaries_ {#stack-canaries}

One of the most important buffer overflow attacks is the first Internet worm, written by Robert Morris Jr. in 1988\. It modified the return address on the stack, injected malicious code, then it controlled the system. (See figure 1-1 Stack Smashing Buffer Overflow Attack)

![](Mydir/media/image1.png)

Figure 1-1 Stack Smashing Buffer Overflow Attack (Source: [StackCheck])

In 1999, StackCheck was introduced to prevent buffer overflow attack on a stack. [StackCheck]

When the program makes a function call, it puts a random digital canary on top of the return address on the stack. When the function returns, the program checks if the canary data is modified. If it is modified, there must be something wrong and a special failure reporting function is invoked before the program returns back to the function address on the stack. (See figure 1-2 Canary Word Next to Return Address)

![](Mydir/media/image2.png)

Figure 1-2 Canary Word Next to Return Address (Source: [StackGuard])

Stack canary is a software feature. It is supported by most compilers.