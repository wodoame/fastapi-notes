When you use the `dependencies` keyword argument in `app.get()` (or any route decorator) in FastAPI, you specify a list of dependencies that will be **executed before the endpoint runs**, but **their return values are not passed to your endpoint function**.

**Purpose:**  
- To run logic such as authentication, authorization, or logging before the endpoint executes.
- To enforce side effects or checks (e.g., user must be authenticated).

**Example:**
```python
@app.get("/items/", dependencies=[Depends(authenticate_user)])
def read_items():
    return ["item1", "item2"]
```
Here, `authenticate_user` will run before `read_items`, but its result is not passed to `read_items`.

**Summary:**  
`dependencies` is for running dependencies for their side effects, not for injecting their return values into your endpoint function.
