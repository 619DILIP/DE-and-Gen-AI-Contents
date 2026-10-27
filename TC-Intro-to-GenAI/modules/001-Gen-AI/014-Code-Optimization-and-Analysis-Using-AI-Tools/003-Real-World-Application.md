## Investigating a Slow Report

A nightly report that used to finish in minutes now takes over an hour, and the data volume has grown considerably since it was written.

Asking a tool to make the report faster without more information invites guesses at whatever looks worst. Profiling first shows that almost all the time sits in one function, which turns out to query the database once per row rather than once for the whole set. That specific function is then the thing to hand over for analysis, and the suggestion, batching the lookups into a single query, addresses the actual cause.

The report's existing tests confirm the output is unchanged, and a second timing run confirms the improvement is real. Every other candidate the tool might have flagged in a broader review would have been a distraction, because none of them accounted for meaningful runtime.