## Testing a Pipeline Without Its Dependencies

An extraction function that pulls data from a partner's API and writes it to storage has two external dependencies, neither of which should be involved in a unit test. The partner's API should not be called on every test run, and no test should write real objects into real storage.

Mocking both allows the function's actual logic to be verified: that it requests the right endpoint, that it handles a well-formed response correctly, that it skips malformed records rather than crashing, and that it retries or raises appropriately when the service returns an error. All of that is tested in milliseconds, on any machine, with no credentials and no network.

The same reasoning applies to a function that writes to a cloud service. Mocking the client verifies that the correct call would be made, with the correct arguments, without anything actually being created.