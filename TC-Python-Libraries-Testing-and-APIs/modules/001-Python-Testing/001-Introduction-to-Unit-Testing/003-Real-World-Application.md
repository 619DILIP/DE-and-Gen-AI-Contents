## Testing in a Development Workflow

In most professional teams, code is not considered complete until it has tests. When a developer submits a change, an automated system typically runs the full test suite before that change is allowed to merge. If a test fails, the change is blocked until it is fixed.

This matters most on teams where many people work on the same codebase. A developer changing one part of an application cannot manually check every other part that might depend on it, but a test suite can check all of it in seconds. This is why unit testing is treated as a core skill rather than an optional add on, regardless of the language or framework a team uses.