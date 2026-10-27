<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

* Explain what an API is and why data systems expose one.
* Describe how FastAPI relates to HTTP methods, paths, and status codes.
* Read and explain a basic FastAPI application.
* Distinguish path parameters, query parameters, and request bodies.
* Explain how Pydantic models validate incoming and outgoing data.
* Describe how an API endpoint connects to a database.
* Recognize the role of automatic interactive documentation.
* Run a FastAPI application using the FastAPI CLI.
* Test FastAPI endpoints using the built-in test client.

</details>

<details><summary>Description</summary>

## What is FastAPI

FastAPI is a Python web framework for building APIs. It is widely used because it combines a small amount of code with two things that would otherwise take significant effort:

* **Automatic validation.** Incoming data is checked against a declared structure, and a clear error is returned when it does not match.
* **Automatic documentation.** An interactive documentation page is generated from the code itself, so it stays synchronized with the API definition.

Both come from FastAPI's use of Python type hints and Pydantic models. The types and models written for clarity also drive the behavior of the application.

FastAPI is built on top of **Starlette** for web functionality and **Pydantic** for data validation and serialization.

---

## HTTP Basics

An API endpoint is identified by a method and a path.

| Method | Conventional meaning              |
| ------ | --------------------------------- |
| GET    | Retrieve data, changing nothing   |
| POST   | Create something new              |
| PUT    | Replace an existing item          |
| PATCH  | Partially update an existing item |
| DELETE | Remove an item                    |

Responses carry a status code indicating the outcome:

| Code | Meaning                           |
| ---- | --------------------------------- |
| 200  | Success                           |
| 201  | Created successfully              |
| 400  | The request was malformed         |
| 404  | The requested item does not exist |
| 422  | The request failed validation     |
| 500  | The server encountered an error   |

These conventions are not enforced by anything technical, but following them is what makes an API predictable to anyone consuming it.

---

## A Minimal Application

```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
def read_root():
    return {"status": "ok"}


@app.get("/health")
def health_check():
    return {"status": "healthy", "service": "sales-api"}
```

Three things are happening:

1. `FastAPI()` creates the application.
2. The `@app.get("/health")` decorator registers the function below it to handle GET requests to that path.
3. The returned dictionary is automatically converted to JSON.

### Running the Application

With a project managed by `uv`, start the development server with:

```text
uv run fastapi dev
```

The FastAPI CLI automatically detects the application in `main.py` when it finds an object named `app`.

By default, development mode enables automatic reloading and listens on `127.0.0.1`, making the application available only from the local machine.

For example:

```text
FastAPI
    ↓
FastAPI CLI
    ↓
Uvicorn
    ↓
ASGI
    ↓
HTTP requests
```

FastAPI CLI uses Uvicorn as the underlying ASGI server.

For production, use:

```text
uv run fastapi run
```

Unlike development mode, production mode does not enable automatic reloading by default.

The lower-level Uvicorn command is still useful when you need direct control over the ASGI server:

```text
uv run uvicorn main:app
```

Here, `main:app` means:

* `main` is the Python module represented by `main.py`.
* `app` is the FastAPI application object created with `app = FastAPI()`.

---

## Path Parameters

A path parameter captures a value from the URL itself, used to identify a specific resource.

```python
@app.get("/products/{product_id}")
def get_product(product_id: int):
    return {"product_id": product_id}
```

Requesting `/products/42` calls the function with `product_id` set to `42`.

The `int` type hint is doing real work: FastAPI validates the incoming value and returns a validation error if it is not a valid integer, without any manual checking.

---

## Query Parameters

Query parameters appear after a question mark and are typically used for filtering, sorting, and pagination. Any function argument that does not match a path parameter becomes a query parameter.

```python
@app.get("/products")
def list_products(category: str | None = None, limit: int = 10):
    return {"category": category, "limit": limit}
```

Requesting:

```text
/products?category=tools&limit=25
```

supplies both parameters.

Arguments with defaults are optional. Arguments without defaults are required, and FastAPI returns a validation error when a required parameter is missing.

---

## Request Bodies and Pydantic

For creating or updating resources, data commonly comes in the request body as JSON. The expected structure is declared as a Pydantic model, which is a class describing the fields and their types.

```python
from fastapi import FastAPI
from pydantic import BaseModel, Field

app = FastAPI()


class ProductCreate(BaseModel):
    name: str
    price: float = Field(gt=0)
    quantity: int = Field(ge=0)
    category: str | None = None


@app.post("/products", status_code=201)
def create_product(product: ProductCreate):
    return {
        "created": product.name,
        "price": product.price
    }
```

The model does a substantial amount of work automatically.

Incoming JSON is parsed and checked against the declared types and constraints. A missing `name`, a `price` of zero or below, or an invalid `quantity` produces a validation response describing which field failed and why, before the function body runs.

This is the part worth appreciating. Validation logic that would otherwise require many lines of manual checking is expressed as a model definition, and that same definition is also used to generate the API documentation.

---

## Response Models

The same idea applies to what goes out. Declaring a response model controls the shape of the response and helps prevent accidentally exposing fields that should remain internal.

```python
class ProductOut(BaseModel):
    id: int
    name: str
    price: float


@app.get("/products/{product_id}", response_model=ProductOut)
def get_product(product_id: int):
    record = fetch_from_database(product_id)
    return record
```

If `fetch_from_database` returns extra fields, such as an internal cost or a supplier ID, FastAPI uses the declared response model to control the response data.

This is a meaningful safeguard rather than merely a convenience.

---

## Automatic Documentation

Because the routes, parameters, and models are declared in code, FastAPI generates interactive documentation automatically.

Running the application and visiting:

```text
http://127.0.0.1:8000/docs
```

opens an interactive documentation page listing every endpoint, its parameters, its expected request body, and its response shape. You can select an endpoint and send test requests directly from the browser.

An alternative documentation view is available at:

```text
http://127.0.0.1:8000/redoc
```

Both interfaces are generated from the same OpenAPI specification.

The OpenAPI specification itself is available as JSON at:

```text
http://127.0.0.1:8000/openapi.json
```

This specification can also be consumed by tools that generate API clients or other documentation.

This matters practically because API documentation that lives separately from the code can become stale. Generating it from the application definition keeps the documentation synchronized with the API.

---

</details>

<details><summary>Real World Application</summary>

## Serving Warehouse Data

A common pattern places an API in front of a data warehouse. The warehouse holds aggregated sales figures, and several consumers need them: an internal dashboard, a partner's system, and a mobile application.

Rather than granting each consumer direct database access, a small API exposes a handful of endpoints such as:

* Revenue by region
* Revenue by month
* Product performance
* Customer summaries

That arrangement means database credentials are held in one place, access can be logged and rate limited, the query logic is written once rather than reimplemented by each consumer, and the underlying warehouse can be changed or migrated without each consumer needing to know.

The same skill applies in reverse during extraction. Pulling data from an external source frequently means consuming that source's API, and having built one makes reading someone else's API documentation considerably easier.

</details>

<details><summary>Implementation</summary>

## Installing

This course uses `uv` to manage the Python project, dependencies, and virtual environment.

Create a new project if one does not already exist:

```text
uv init sales-api --bare
cd sales-api
```

Then add FastAPI:

```text
uv add "fastapi[standard]"
```

The quotes around `"fastapi[standard]"` are intentional. They ensure the command works consistently across different terminals and shells.

The `fastapi[standard]` extra installs FastAPI together with its standard optional dependencies. These include:

* `uvicorn[standard]` for serving the application.
* `fastapi-cli[standard]` for the `fastapi` command.
* `httpx`, which is required by FastAPI's `TestClient`.
* `python-multipart`, which supports form-data parsing.
* `jinja2`, which supports the default template configuration.
* Other standard dependencies used by FastAPI and its underlying libraries.

The project will contain:

```text
sales-api/
├── .venv/
├── pyproject.toml
└── uv.lock
```

`pyproject.toml` records the project's declared dependencies.

`uv.lock` records the resolved versions so that the same dependency versions can be installed later.

The `.venv` directory contains the project's virtual environment.

You do not need to create or activate the virtual environment manually when using `uv` for this workflow.

---

## Running the Application

Create a file named `main.py`:

```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
def read_root():
    return {"status": "ok"}


@app.get("/health")
def health_check():
    return {
        "status": "healthy",
        "service": "sales-api"
    }
```

Start the development server:

```text
uv run fastapi dev
```

The FastAPI CLI searches for the application and automatically starts it using Uvicorn.

The application will normally be available at:

```text
http://127.0.0.1:8000
```

The interactive documentation is available at:

```text
http://127.0.0.1:8000/docs
```

The alternative documentation is available at:

```text
http://127.0.0.1:8000/redoc
```

---

## Project Structure

A small API can initially start with a single `main.py` file. As the application grows, responsibilities can be separated into multiple modules.

A simple structure might look like:

```text
sales-api/
├── main.py
├── models.py
├── database.py
├── pyproject.toml
└── uv.lock
```

For example:

```text
main.py
    application and routes

models.py
    Pydantic request and response models

database.py
    database connection and query handling

pyproject.toml
    project metadata and dependencies

uv.lock
    exact resolved dependency versions
```

A larger application can later use packages and multiple routers.

---

## Configuring the Application Entrypoint

For a simple application, the FastAPI CLI can automatically find an application named `app` in `main.py`.

For larger applications, the location of the application can be declared explicitly in `pyproject.toml`.

For example:

```toml
[tool.fastapi]
entrypoint = "main:app"
```

If the application is located at:

```text
backend/
└── main.py
```

the entrypoint could be:

```toml
[tool.fastapi]
entrypoint = "backend.main:app"
```

This tells the FastAPI CLI which application object to run.

---

## A Complete Example

Bringing together routes, validation, and a database connection.

### `models.py`

```python
from pydantic import BaseModel, Field


class ProductCreate(BaseModel):
    name: str = Field(min_length=1, max_length=100)
    price: float = Field(gt=0)
    quantity: int = Field(ge=0)


class ProductOut(BaseModel):
    id: int
    name: str
    price: float
    quantity: int
```

### `main.py`

```python
import os
import sqlite3

from fastapi import FastAPI, HTTPException

from models import ProductCreate, ProductOut


app = FastAPI(
    title="Sales API",
    version="1.0"
)


DB_PATH = os.environ.get("DB_PATH", "sales.db")


def get_connection():
    conn = sqlite3.connect(DB_PATH)
    conn.row_factory = sqlite3.Row
    return conn


@app.get("/health")
def health():
    return {"status": "healthy"}


@app.get("/products", response_model=list[ProductOut])
def list_products(
    limit: int = 20,
    min_price: float = 0
):
    conn = get_connection()

    rows = conn.execute(
        "SELECT id, name, price, quantity "
        "FROM products "
        "WHERE price >= ? LIMIT ?",
        (min_price, limit)
    ).fetchall()

    conn.close()

    return [dict(row) for row in rows]


@app.get(
    "/products/{product_id}",
    response_model=ProductOut
)
def get_product(product_id: int):
    conn = get_connection()

    row = conn.execute(
        "SELECT id, name, price, quantity "
        "FROM products "
        "WHERE id = ?",
        (product_id,)
    ).fetchone()

    conn.close()

    if row is None:
        raise HTTPException(
            status_code=404,
            detail="Product not found"
        )

    return dict(row)


@app.post(
    "/products",
    response_model=ProductOut,
    status_code=201
)
def create_product(product: ProductCreate):
    conn = get_connection()

    cursor = conn.execute(
        "INSERT INTO products (name, price, quantity) "
        "VALUES (?, ?, ?)",
        (
            product.name,
            product.price,
            product.quantity
        )
    )

    conn.commit()

    new_id = cursor.lastrowid

    conn.close()

    return {
        "id": new_id,
        **product.model_dump()
    }
```

Several practices from earlier modules appear here.

Queries use parameter placeholders rather than string formatting, which prevents SQL injection.

The database path comes from an environment variable rather than being hardcoded.

`HTTPException` returns a proper 404 when a requested record does not exist rather than allowing the missing record to become an unexpected server error.

Pydantic models validate incoming data before the endpoint function processes it.

The response model controls which fields are returned to the client.

---

## Returning Aggregated Data

An endpoint serving warehouse-style summaries follows the same basic shape.

```python
@app.get("/revenue/by-region")
def revenue_by_region(year: int | None = None):
    conn = get_connection()

    sql = """
        SELECT
            region,
            SUM(revenue) AS total_revenue,
            COUNT(*) AS order_count
        FROM fact_sales f
        JOIN dim_customer c
            ON f.customer_id = c.customer_id
        GROUP BY region
        ORDER BY total_revenue DESC
    """

    rows = conn.execute(sql).fetchall()

    conn.close()

    return [dict(row) for row in rows]
```

The SQL is the same fact-and-dimension join covered in the data warehousing material. The API is simply a delivery mechanism for the resulting data.

The API does not replace the data warehouse. It provides a controlled interface through which other systems can consume selected data.

---

## Testing an Endpoint

FastAPI provides a `TestClient` that can be used with the testing tools covered earlier.

Because the project was installed with:

```text
uv add "fastapi[standard]"
```

the standard installation includes `httpx`, which is required for `TestClient`.

A test file can be created as `test_main.py`:

```python
from fastapi.testclient import TestClient

from main import app


client = TestClient(app)


def test_health():
    response = client.get("/health")

    assert response.status_code == 200
    assert response.json()["status"] == "healthy"


def test_get_missing_product_returns_404():
    response = client.get("/products/999999")

    assert response.status_code == 404


def test_create_product_rejects_negative_price():
    response = client.post(
        "/products",
        json={
            "name": "Widget",
            "price": -5,
            "quantity": 10
        }
    )

    assert response.status_code == 422
```

The last test demonstrates Pydantic validation working through FastAPI.

No manual check for a negative price was written in the endpoint. The constraint:

```python
price: float = Field(gt=0)
```

declares that the value must be greater than zero.

FastAPI validates the request against the model before the endpoint function executes.

Run the tests with:

```text
uv run pytest
```

---

## Exploring the Documentation

1. Start the development server:

   ```text
   uv run fastapi dev
   ```

2. Open:

   ```text
   http://127.0.0.1:8000/docs
   ```

3. Every endpoint is listed with its parameters and expected request body.

4. Select an endpoint and choose **Try it out**.

5. Enter any required parameters or request body data.

6. Execute the request.

7. Inspect the HTTP status code and JSON response.

8. Open `/redoc` to see the alternative documentation interface.

9. Open `/openapi.json` to inspect the generated OpenAPI specification directly.

---

## FastAPI CLI and Uvicorn

The FastAPI CLI is the recommended high-level interface for running a FastAPI application during development.

```text
uv run fastapi dev
```

Internally, the FastAPI CLI uses Uvicorn, which is an ASGI server.

The relationship is:

```text
FastAPI application
        ↓
FastAPI CLI
        ↓
Uvicorn
        ↓
ASGI
        ↓
HTTP server
```

You can also run Uvicorn directly when you need more explicit server configuration:

```text
uv run uvicorn main:app
```

For example:

```text
uv run uvicorn main:app --host 0.0.0.0 --port 8000
```

The direct Uvicorn command is not obsolete. It is simply a lower-level way to run the application.

For normal local development in this course, use:

```text
uv run fastapi dev
```

---

## Development vs Production

Development mode:

```text
uv run fastapi dev
```

is intended for local development.

It enables automatic reload by default, so changes to the source code cause the development server to restart.

Production mode:

```text
uv run fastapi run
```

does not enable automatic reload by default.

Automatic reload is useful during development but consumes additional resources and should not be enabled as a production configuration.

---

## Steps to Follow

1. Create or enter the `uv` project.

2. Add FastAPI with:

   ```text
   uv add "fastapi[standard]"
   ```

3. Create the application object with `FastAPI()`.

4. Define routes using the appropriate HTTP method.

5. Declare path and query parameter types.

6. Define Pydantic models for request bodies.

7. Define response models to control the data returned.

8. Start the development server with:

   ```text
   uv run fastapi dev
   ```

9. Use parameterized SQL queries when interacting with databases.

10. Read database configuration from environment variables rather than hardcoding credentials or environment-specific values.

11. Raise `HTTPException` with an appropriate status code for expected failure cases.

12. Test endpoints with `TestClient`.

13. Run the test suite with:

```text
uv run pytest
```

14. Check the generated documentation at `/docs`.
15. Use `/openapi.json` when you need to inspect the generated API specification.

</details>

<details><summary>Summary</summary>

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

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
