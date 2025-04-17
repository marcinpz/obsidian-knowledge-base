# FastAPI Overview

FastAPI is a modern, fast (high-performance), web framework for building APIs with Python 3.7+ based on standard Python type hints.

## 🔥 Key Features

- **Fast**: One of the fastest Python frameworks available, thanks to Starlette and Pydantic.
- **Pythonic**: Designed to be intuitive and easy to use with Python.
- **Automatic docs**: Swagger UI and ReDoc auto-generated from your code.
- **Type checking**: Full support for type hints, autocompletion, and static analysis.
- **Asynchronous**: Full async/await support.

## 🚀 Getting Started

### Installation

```bash
pip install fastapi[all]
```

This includes Uvicorn, an ASGI server for running your app.

### Hello World Example

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello, World!"}
```

To run:

```bash
uvicorn main:app --reload
```

## 📚 Path Parameters and Query Parameters

```python
@app.get("/items/{item_id}")
def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "query": q}
```

## 🧾 Request Body

```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    price: float
    is_offer: bool = None

@app.post("/items/")
def create_item(item: Item):
    return {"item": item}
```

## 🛡️ Dependency Injection

```python
from fastapi import Depends

def common_parameters(q: str = None):
    return {"q": q}

@app.get("/search")
def search(params: dict = Depends(common_parameters)):
    return params
```

## 📃 Auto-generated Documentation

- Swagger UI: `http://localhost:8000/docs`
- ReDoc: `http://localhost:8000/redoc`

## ✅ Use Cases

- REST APIs
- Microservices
- Machine Learning model serving
- Serverless backends

## 🔗 Related Tools

- **Uvicorn**: ASGI server to run FastAPI apps.
- **Pydantic**: Data validation and settings management using Python type annotations.
- **SQLAlchemy / Tortoise ORM**: Database integration.

---

tags: #fastapi #python #backend #api #web-development
