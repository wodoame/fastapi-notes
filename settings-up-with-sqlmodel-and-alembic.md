Here’s a step-by-step guide to set up a FastAPI project using **SQLModel** (for ORM) and **Alembic** (for migrations):

---

### 1. Create and Activate a Virtual Environment

```powershell
python -m venv venv
.\venv\Scripts\activate
```

---

### 2. Install Dependencies

```powershell
pip install fastapi uvicorn sqlmodel alembic
```

---

### 3. Create Project Structure

Example:
```
fastapiproject/
│
├── app/
│   ├── __init__.py
│   ├── main.py
│   ├── models.py
│   └── database.py
├── alembic.ini
└── ...
```

---

### 4. Create SQLModel Models

```python
from sqlmodel import SQLModel, Field

class User(SQLModel, table=True):
    id: int | None = Field(default=None, primary_key=True)
    name: str
    email: str
```

---

### 5. Set Up Database Connection

```python
from sqlmodel import SQLModel, create_engine

DATABASE_URL = "sqlite:///./test.db"
engine = create_engine(DATABASE_URL, echo=True)
```

---

### 6. Create FastAPI App

```python
from fastapi import FastAPI
from app.models import User
from app.database import engine, SQLModel

app = FastAPI()

@app.on_event("startup")
def on_startup():
    SQLModel.metadata.create_all(engine)

@app.get("/")
def read_root():
    return {"Hello": "World"}
```

---

### 7. Initialize Alembic

```powershell
alembic init alembic
```


- Edit alembic.ini and set `sqlalchemy.url = sqlite:///./test.db`
- In env.py, import your models and set target metadata:
- Edit the script.py.mako file to import sqlmodel

```python
from app.models import SQLModel
target_metadata = SQLModel.metadata
```

---

### 8. Create and Run Migrations

```powershell
alembic revision --autogenerate -m "Initial migration"
alembic upgrade head
```

---

### 9. Run the FastAPI App

```powershell
uvicorn app.main:app --reload
```

---

**You now have a FastAPI project with SQLModel and Alembic for migrations!**  
