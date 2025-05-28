In FastAPI, `Depends` is used for **dependency injection**. It allows you to declare dependencies (such as functions, classes, or callables) that should be executed and their results provided to your path operation functions (endpoints) or other dependencies.

**Example:**
```python
from fastapi import Depends

def get_db():
    # return a database session
    ...

@app.get("/items/")
def read_items(db = Depends(get_db)):
    # db is provided by get_db
    ...
```

**Summary:**  
`Depends` tells FastAPI to call the dependency, resolve its return value, and pass it as an argument to your endpoint or another dependency. This is useful for authentication, database sessions, and reusable logic.
