In this module, we learned:

- A fixture holds shared test setup in one place, and tests request it by declaring its name as a parameter.
- Scope controls how often a fixture is recreated, trading speed against isolation between tests.
- `yield` splits a fixture into setup and teardown, with teardown running even when a test fails.
- Fixtures can depend on other fixtures, which are resolved and torn down in the correct order.
- `conftest.py` shares fixtures across test files without any import.
- Parameterization runs one test against many inputs, reporting each case separately.
- Test data can be externalized to JSON or CSV so cases can be added without changing code.

These techniques are what make a test suite maintainable once it grows beyond a handful of simple assertions.