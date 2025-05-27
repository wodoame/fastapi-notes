In FastAPI, the **request object** represents the incoming HTTP request. It provides access to details such as headers, cookies, query parameters, the request body, and more.

You can access the request object by adding a parameter of type `Request` from `fastapi` (which is actually imported from `starlette.requests`) to your endpoint function.

**Example:**
````python
from fastapi import FastAPI, Request

app = FastAPI()

@app.get("/info")
async def get_info(request: Request):
    client_host = request.client.host
    headers = dict(request.headers)
    return {"client_host": client_host, "headers": headers}
````

**Common uses:**
- Accessing request headers, cookies, or query parameters.
- Reading the raw request body (with `await request.body()`).
- Getting client information.

**Note:**  
The request object is especially useful for middleware, dependency injection, or when you need low-level access to the HTTP request.
