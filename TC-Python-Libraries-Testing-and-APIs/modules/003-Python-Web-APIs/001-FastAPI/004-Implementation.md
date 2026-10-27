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