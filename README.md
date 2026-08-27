# LangChainUpdated

A Python-based environment for experimenting with **LangChain, LLMs, APIs, and AI application development**.

This project uses **uv** for Python project and dependency management and **Jupyter Notebook** for interactive development and experimentation.

---

## 1. Install `uv`

`uv` is a fast Python package and project manager developed by Astral.

### macOS — Homebrew

```bash
brew install uv
```

Verify the installation:

```bash
uv --version
```

Alternatively, `uv` can be installed using the official installer:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

If the terminal does not recognize `uv` after installation, restart the terminal or reload your shell configuration.

---

## 2. Initialize the Project

Navigate to the folder where you want to create the project:

```bash
cd <project-folder>
```

Initialize a new `uv` project:

```bash
uv init
```

This creates the basic Python project structure.

For example:

```text
langchainupdated/
├── .python-version
├── README.md
├── main.py
├── pyproject.toml
└── uv.lock
```

### `pyproject.toml`

The `pyproject.toml` file contains the project's configuration and dependency information.

It can include:

* Python version
* Project metadata
* Project dependencies
* Development dependencies
* Build configuration

The `uv.lock` file locks dependency versions to provide reproducible installations.

---

## 3. Create a Virtual Environment

Create a virtual environment:

```bash
uv venv
```

This creates:

```text
.venv/
```

Activate the virtual environment:

```bash
source .venv/bin/activate
```

You should now see the virtual environment reflected in your terminal prompt.

To deactivate it later:

```bash
deactivate
```

> **Note:** `.venv` is the project's virtual environment and should not be committed to GitHub.

---

## 4. Manage Dependencies

There are two common ways to add dependencies.

### Add an individual library

```bash
uv add langchain
```

For example:

```bash
uv add openai
uv add python-dotenv
uv add ipykernel
```

`uv` resolves compatible versions and records the dependencies in `pyproject.toml` and `uv.lock`.

### Install dependencies from `requirements.txt`

If the project already contains a `requirements.txt` file:

```bash
uv add -r requirements.txt
```

This imports the dependencies into the `uv` project.

> **Recommendation:** For a new `uv` project, prefer `uv add <package>` and let `pyproject.toml` and `uv.lock` manage the project's dependencies.

---

## 5. Environment Variables and API Keys

AI applications often require API keys for services such as:

* OpenAI
* Google Gemini
* Groq

Create a `.env` file in the **project root**, not inside `.venv`.

Project structure:

```text
langchainupdated/
├── .env
├── .gitignore
├── .python-version
├── pyproject.toml
├── uv.lock
├── main.py
└── updatedlangchain/
    └── 1-langchainintro.ipynb
```

Example `.env`:

```env
OPENAI_API_KEY=your_openai_api_key
GOOGLE_API_KEY=your_google_api_key
GROQ_API_KEY=your_groq_api_key
```

### Important: Never commit API keys

Add `.env` to `.gitignore`:

```gitignore
.env
.venv/
__pycache__/
*.pyc
.ipynb_checkpoints/
```

Then verify that `.env` is not being tracked:

```bash
git status
```

> **Security warning:** Never paste API keys directly into source code, notebooks, README files, Git commits, or public GitHub repositories.

If an API key has already been exposed publicly, **revoke it and generate a new key immediately**.

---

## 6. Load Environment Variables in Python

Install `python-dotenv`:

```bash
uv add python-dotenv
```

Then use it in Python:

```python
import os
from dotenv import load_dotenv

load_dotenv()

openai_api_key = os.getenv("OPENAI_API_KEY")
google_api_key = os.getenv("GOOGLE_API_KEY")
groq_api_key = os.getenv("GROQ_API_KEY")
```

You can verify that the variables are loaded without printing the actual keys:

```python
if openai_api_key:
    print("OpenAI API key loaded")

if google_api_key:
    print("Google API key loaded")

if groq_api_key:
    print("Groq API key loaded")
```

### Do not do this

```python
print(os.getenv("OPENAI_API_KEY"))
```

Never print secret credentials in logs, notebooks, screenshots, or GitHub commits.

---

## 7. Set Up Jupyter Notebook

Jupyter Notebook provides an interactive environment for experimenting with Python and AI applications.

Install `ipykernel`:

```bash
uv add ipykernel
```

You can then create notebooks inside the project.

For example:

```text
updatedlangchain/
└── 1-langchainintro.ipynb
```

Open the project in VS Code:

```bash
code .
```

Open:

```text
updatedlangchain/1-langchainintro.ipynb
```

Select the project's `.venv` Python environment as the notebook kernel.

---

## 8. First Jupyter Notebook

In `1-langchainintro.ipynb`, load the environment variables:

```python
import os
from dotenv import load_dotenv

load_dotenv()
```

Then access an API key:

```python
openai_api_key = os.getenv("OPENAI_API_KEY")
```

For Google:

```python
google_api_key = os.getenv("GOOGLE_API_KEY")
```

For Groq:

```python
groq_api_key = os.getenv("GROQ_API_KEY")
```

The notebook can now use these credentials when initializing the respective LLM clients.

---

## 9. Adding New Libraries

When you need a new Python library, the recommended approach is:

```bash
uv add <library-name>
```

For example:

```bash
uv add langchain
```

```bash
uv add langchain-openai
```

```bash
uv add langchain-google-genai
```

```bash
uv add langchain-groq
```

This updates the project's dependency configuration and lock file.

If you already have the dependency listed in `requirements.txt`, you can instead run:

```bash
uv add -r requirements.txt
```

---

## 10. Useful `uv` Commands

### Check `uv` version

```bash
uv --version
```

### Initialize a project

```bash
uv init
```

### Create a virtual environment

```bash
uv venv
```

### Activate the environment

```bash
source .venv/bin/activate
```

### Add a package

```bash
uv add <package-name>
```

### Add packages from requirements.txt

```bash
uv add -r requirements.txt
```

### Install/synchronize project dependencies

```bash
uv sync
```

### Run Python through the project environment

```bash
uv run python
```

### Run a Python file

```bash
uv run main.py
```

---

## 11. Recommended Project Structure

A clean structure for this project is:

```text
langchainupdated/
│
├── .env
├── .gitignore
├── .python-version
├── README.md
├── main.py
├── pyproject.toml
├── uv.lock
│
└── updatedlangchain/
    └── 1-langchainintro.ipynb
```

As the project grows, it can evolve into:

```text
langchainupdated/
│
├── .env
├── .gitignore
├── README.md
├── pyproject.toml
├── uv.lock
│
├── notebooks/
│   ├── 01_langchain_intro.ipynb
│   ├── 02_llm_models.ipynb
│   ├── 03_prompts.ipynb
│   └── 04_rag.ipynb
│
├── src/
│   └── langchainupdated/
│       ├── __init__.py
│       ├── models.py
│       ├── prompts.py
│       └── rag.py
│
└── tests/
```

---

## 12. Typical Development Workflow

The overall workflow is:

```text
Install uv
     ↓
uv init
     ↓
Create virtual environment
     ↓
uv venv
     ↓
Activate .venv
     ↓
Install dependencies
     ↓
uv add <package>
     ↓
Create .env
     ↓
Add API credentials
     ↓
Install ipykernel
     ↓
Create Jupyter Notebook
     ↓
Experiment with LangChain / LLMs
     ↓
Move stable code into Python modules
     ↓
Build and test the application
```

### Quick Start

For a new project, the essential commands are:

```bash
brew install uv

uv init

uv venv

source .venv/bin/activate

uv add python-dotenv

uv add ipykernel

uv sync
```

Then create your `.env` file, configure your API keys securely, and open the project in VS Code.

