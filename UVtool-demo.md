# FastAPI + UV Demo 🚀

This project is a simple demonstration of how to set up and run a FastAPI application using [uv](https://github.com/astral-sh/uv), an extremely fast Python package and project manager written in Rust.

## What is `uv`?
Think of `uv` as a lightning-fast replacement for `pip`, `venv`, and `poetry`. It manages your Python versions, creates virtual environments, installs dependencies, and locks them to specific versions so your project works reliably everywhere.

---

## 🛠️ Step-by-Step Setup Guide

### Prerequisites
* Python 3.10 or newer
* Docker (optional)
```
curl -LsSf https://astral.sh/uv/install.sh | sh
```
if you are on Windows, you can also run the following command in PowerShell to add uv to your path:
```powershell
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
```
if you want to verify uv installation, you can run the following command:
```bash
uv --version
```
if you want to update uv, you can run the following command:
```bash
uv self update
```

### 1. Initialize the Project
```bash
uv init

```

This sets up a new Python project in the current folder. It automatically creates the core configuration files needed to manage dependencies.

### 2. Create the App

Create a file named `main.py` and add your FastAPI code:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello": "World from FastAPI + UV!"}

```

### 3. Install Dependencies

```bash
uv add fastapi
uv add uvicorn
uv add <package_name>  # Add any other packages you need
```

When you run `uv add`, a few magic things happen instantly:

* It downloads and installs the packages (and their dependencies) in milliseconds.
* It updates your project files to track these new dependencies.

### 4. Verify and Sync (Optional but Good Practice)

To see everything installed in your environment:

```bash
uv pip list

```

To ensure your environment perfectly matches your locked dependencies:

```bash
uv sync

```
* with this command, `uv` detects you need a virtual environment and creates one (`.venv`).

### 5. Run the Server

Use `uv run` to execute commands inside your project's virtual environment without needing to manually "activate" it:

```bash
uv run uvicorn main:app --reload

```

Your app is now running at `http://127.0.0.1:8000`!

---

## 📁 What Are All These Files?

When you initialize and add packages with `uv`, it generates a few key files. Here is what they do:

* **`main.py`**: Your actual application code.
* **`pyproject.toml`**: The blueprint of your project. It lists your project name, Python version requirement, and the primary dependencies (like `fastapi` and `uvicorn`).
* **`uv.lock`**: The exact blueprint. It records the exact version of *every* sub-dependency installed (like `starlette`, `pydantic`, etc.) so that anyone else running your code gets the exact same setup.
* **`.venv/`** (hidden folder): Your virtual environment. This is where the actual Python files for your installed packages live. You should never commit this to GitHub.