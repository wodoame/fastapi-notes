The `Path` class in FastAPI is used to declare and validate parameters that are part of the URL path. It allows you to add metadata, set default values, and perform validation (like minimum/maximum values) for path parameters.

**Example usage:**
````python
from fastapi import FastAPI, Path

app = FastAPI()

@app.get("/items/{item_id}")
async def read_item(item_id: int = Path(..., title="The ID of the item", ge=1)):
    return {"item_id": item_id}
````

- `...` means the parameter is required.
- `title` adds documentation.
- `ge=1` means the value must be greater than or equal to 1.

`Path` is similar to `Query` and `Body`, but specifically for path parameters.
