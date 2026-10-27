## Running Tests as Part of a Build

In a real project, tests are rarely run only by hand. They are wired into an automated pipeline that runs every time code is pushed to a shared repository. If a `pytest` or `unittest` run fails, the pipeline marks the change as broken and blocks it from being merged until the tests pass again. This is what allows teams with many contributors to change shared code confidently, since a broken test is caught within minutes of being introduced rather than being discovered later.
