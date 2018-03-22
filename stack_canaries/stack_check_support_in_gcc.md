## Stack Check Support in GCC {#stack-check-support-in-gcc}

The first stack guard is supported in GCC. Current GCC supports:  -fstack-protector, -fstack-protector-all, and -fstack-protector-strong. [StackCanaries].

-fstack-protector-strong is recommended because “this option tries to hit the balance between an over-simplified version and an over-killing protection schema”. [GCC]