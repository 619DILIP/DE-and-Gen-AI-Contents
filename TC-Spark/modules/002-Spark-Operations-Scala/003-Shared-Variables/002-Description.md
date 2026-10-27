# Introduction to Shared Variable 

- Shared variable is used to executes on the specific remote cluster node. Usually, it works on separate copies of all the variables those we use in functions. These specific variables are precisely copied to each machine.

- Shared variables are used to save the state, either at the module level or for the duration of a job. Using shared variables, we can share data across process instances associated with a module or a job. A process instance can read or update the data stored in a shared variable.

- Shared variables are the variables that are required to be used by many functions & methods in parallel.

- Types of Shared variable 

    1.  Broadcast Variables
    2.  Accumulators