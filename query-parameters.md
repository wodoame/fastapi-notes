In FastAPI, **query parameters** are values passed in the URL after the `?` symbol, typically used to filter or modify the response. They are not part of the path, but are optional or required parameters that follow the endpoint.

**Example:**
````python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/")
async def read_items(skip: int = 0, limit: int = 10):
    return {"skip": skip, "limit": limit}
````

Accessing `/items/?skip=5&limit=20` will set `skip` to 5 and `limit` to 20.

You can use the `Query` class from FastAPI to add validation, metadata, and defaults:

````python
from fastapi import FastAPI, Query

app = FastAPI()

@app.get("/users/")
async def read_users(
    q: str = Query(None, min_length=3, max_length=50, title="Search query")
):
    return {"q": q}
````

- `Query(None, ...)` makes the parameter optional.
- You can set constraints like `min_length`, `max_length`, and add documentation.

**Summary:**  
Query parameters in FastAPI are a flexible way to pass data to your endpoints, with built-in validation and documentation support.
