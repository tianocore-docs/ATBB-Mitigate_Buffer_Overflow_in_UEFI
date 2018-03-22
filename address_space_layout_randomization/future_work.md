## Future work {#future-work}

Entropy bit selection is one important task for randomization. Insufficient entropy may not be able to resist an attack. Too strong entropy may easily exhaust the memory. We might need more work to see what the best entropy bit is for the different execution environments.

Current AslrPkg just selects some important components for randomization as a sample. We might need to evaluate if we need to randomize more components, such as the core protocol handle database, system table, etc.

### Summary {#summary}

This section introduces the address space layout randomization technique and how to enable different randomization features in EDKII.