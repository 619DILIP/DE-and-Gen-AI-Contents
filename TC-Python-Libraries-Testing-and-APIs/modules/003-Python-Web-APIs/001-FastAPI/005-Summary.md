In this module, we learned:

* An API exposes data over HTTP so that consumers do not need direct database access.
* FastAPI is a Python framework for building APIs.
* FastAPI uses Python type hints and Pydantic models to drive validation and documentation.
* Endpoints are defined by an HTTP method and a path.
* Path parameters identify resources, while query parameters are commonly used for filtering, sorting, and pagination.
* Request bodies commonly carry JSON data for creating or updating resources.
* Pydantic models declare the expected structure and validation rules for incoming data.
* Response models control the structure of data returned by an endpoint.
* FastAPI automatically generates interactive documentation at `/docs` and `/redoc`.
* OpenAPI describes the API in a machine-readable format at `/openapi.json`.
* `uv` can manage the project, dependencies, virtual environment, and lockfile.
* `fastapi[standard]` provides the standard FastAPI tooling, including Uvicorn and the FastAPI CLI.
* `fastapi dev` provides the recommended development workflow.
* Uvicorn is the ASGI server used underneath the FastAPI CLI.
* Endpoints can connect to databases using the same parameterized-query practices covered earlier.
* FastAPI endpoints can be tested using `TestClient` and `pytest`.

An API is the delivery layer for the data the rest of this course produces.