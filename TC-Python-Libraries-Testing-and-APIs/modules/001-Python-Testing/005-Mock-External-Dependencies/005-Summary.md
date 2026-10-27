In this module, we learned:

- Tests should not depend on real external systems, which are slow, unreliable, and not repeatable.
- A mock stands in for a real dependency, returning configured values and recording how it was used.
- `unittest.mock` is part of the standard library and requires no installation.
- `patch` temporarily replaces a name for the duration of a test and restores it afterward.
- Patching targets the name as the module under test looks it up, not where it was originally defined.
- Assertions on a mock can verify that a dependency was called correctly, which is often the real behavior under test.
- `side_effect` simulates failures, making error handling testable without a real outage.
- Over-mocking produces tests that verify structure rather than behavior, so real lightweight dependencies are preferable where practical.

Together with fixtures and parameterization, mocking makes it possible to test code that depends on systems the test cannot or should not reach.