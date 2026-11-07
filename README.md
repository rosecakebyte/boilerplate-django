# Django Web Application Boilerplate

A reusable Django boilerplate designed to get web application projects up and running quickly with minimal configuration.

This project uses `uv` for Python dependency management, Django for the web framework, and `python-dotenv` for environment variable management.

## Features

- Fast Python environment setup with `uv`
- Django web framework
- `.env` support for environment variables
- SQLite database for local development
- Git-ready project structure
- Makefile shortcuts for common commands
- Easy-to-extend configuration for future projects

## Prerequisites

Before getting started, make sure you have the following installed:

- Python 3.12+
- uv
- Git

### 1. Install uv

`uv` is a fast Python package and project manager.

**Linux / macOS / WSL (Ubuntu):**

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Restart your terminal or reload your shell configuration.

**Windows PowerShell:**

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Verify that uv is installed:

```bash
uv --version
```

Verify Python:

```bash
uv python list
```

If uv is not recognized, see the Troubleshooting section.

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git

cd YOUR_REPOSITORY
```

### 2. Initialize the Python project

If the repository does not already contain a `pyproject.toml`:

```bash
uv init
```

If the repository already has a `pyproject.toml`, skip this step.

### 3. Create a virtual environment

```bash
uv venv
```

### 4. Install Django and python-dotenv

Use uv to add the dependencies:

```bash
uv add django python-dotenv
```

This command adds the dependencies to `pyproject.toml` and updates `uv.lock`.

### 5. Activate the virtual environment (optional)

**Linux / macOS / WSL:**

```bash
source .venv/bin/activate
```

**Windows PowerShell:**

```powershell
.venv\Scripts\Activate.ps1
```

You can also execute Python commands without activating the environment by using `uv run`.

### 6. Start the Django project

If a Django project has not already been created:

```bash
uv run django-admin startproject config .
```

The `config` directory contains the main Django settings, URL configuration, and application entry point.

### 7. Run database migrations

```bash
uv run python manage.py migrate
```

### 8. Start the development server

```bash
uv run python manage.py runserver
```

Open the application:

http://127.0.0.1:8000/

## Environment Variables

### What is python-dotenv?

`python-dotenv` is a Python package that loads environment variables from a `.env` file into your application's environment.

This is useful for storing configuration separately from application code.

Common use cases include:

- Database credentials
- API keys
- Django secret keys
- Debug settings
- External service URLs
- Third-party authentication credentials

### 1. Create a .env file

Create a `.env` file in the root directory:

```env
SECRET_KEY=replace-with-your-secret-key
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
```

### 2. Load environment variables

In `config/settings.py`, add:

```python
import os
from dotenv import load_dotenv

load_dotenv()

SECRET_KEY = os.getenv("SECRET_KEY")

DEBUG = os.getenv("DEBUG", "False").lower() == "true"

ALLOWED_HOSTS = os.getenv(
    "ALLOWED_HOSTS",
    "localhost,127.0.0.1"
).split(",")
```

Now Django can read configuration values from your `.env` file.

### 3. Protect your environment variables

Add the following to `.gitignore`:

```gitignore
# Environment variables
.env

# Virtual environment
.venv/

# Python cache
__pycache__/
*.py[cod]

# Django generated files
db.sqlite3
staticfiles/
media/
```

Never commit API keys, passwords, or production secret keys to GitHub.

## Creating a Django Application

To create a new application:

```bash
uv run python manage.py startapp core
```

Add the application to `INSTALLED_APPS` in `config/settings.py`:

```python
INSTALLED_APPS = [
    # Django built-in apps
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",

    # Custom apps
    "core",
]
```

## Common Commands

| Command | Description |
|---|---|
| `uv sync` | Install project dependencies |
| `uv add django` | Add Django |
| `uv add python-dotenv` | Add python-dotenv |
| `uv run python manage.py runserver` | Start the development server |
| `uv run python manage.py migrate` | Apply database migrations |
| `uv run python manage.py makemigrations` | Create migrations |
| `uv run python manage.py createsuperuser` | Create an admin account |
| `uv run python manage.py startapp core` | Create a Django application |
| `uv run python manage.py test` | Run Django tests |
| `uv run python manage.py check` | Check Django configuration |

## Troubleshooting

### uv: command not found

Check whether uv is installed:

```bash
uv --version
```

If the command fails, install uv:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Restart your terminal.

If you are using Ubuntu or WSL, ensure the uv executable directory is included in your PATH.

### Django is not installed

Install Django using uv:

```bash
uv add django
```

If the project dependencies are already defined:

```bash
uv sync
```

Verify the installation:

```bash
uv run django-admin --version
```

### python-dotenv is not installed

Install the package using uv:

```bash
uv add python-dotenv
```

Verify:

```bash
uv run python -c "import dotenv; print('python-dotenv installed')"
```

### .env variables are not loading

Check the following:

1. Ensure `.env` is located in the project root.
2. Ensure `load_dotenv()` is called before reading environment variables.
3. Verify that variable names match those in `settings.py`.
4. Ensure the `.env` file does not contain invalid syntax.

Example:

```env
DEBUG=True
SECRET_KEY=my-secret-key
```

### ModuleNotFoundError

If Python cannot find a module:

```bash
uv sync
```

If the module is missing from the project dependencies:

```bash
uv add package-name
```

Run the command through uv:

```bash
uv run python manage.py runserver
```

### Database migration errors

Run:

```bash
uv run python manage.py makemigrations
uv run python manage.py migrate
```

### Port 8000 is already in use

Start Django on another port:

```bash
uv run python manage.py runserver 8001
```

## Development Workflow

1. Clone the boilerplate.
2. Run `uv sync`.
3. Configure the `.env` file.
4. Run database migrations.
5. Start the Django development server.
6. Create your Django applications.
7. Begin implementing your features.

## License

MIT License

