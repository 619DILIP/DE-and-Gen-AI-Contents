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