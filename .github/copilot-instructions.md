## Repo overview

This repository contains LangChain experiments and notebooks focused on data ingestion. The primary working notebook is

- `1-Lanchain/3.2-DataIngestion/3.2-DataIngestion.ipynb`

Supporting files:

- `requirements.txt` — Python dependencies for the notebooks.
- `1-Lanchain/3.2-DataIngestion/speech.txt` — sample text data used by `TextLoader` in the notebook.

The codebase is lightweight and notebook-driven. Most development happens by editing and running the Jupyter notebook cells.

## What an AI assistant should know

- This project uses Python notebooks (IPYNB). Edits should maintain notebook JSON structure: code and markdown cells with `metadata.language` set to `python`/`markdown`.
- Primary data flow: the notebook uses `langchain_community.document_loaders.TextLoader` to load `speech.txt` (see cell that does `loader=TextLoader('speech.txt')` and `text_documents=loader.load()`). Keep relative paths (not absolute) so notebooks run from repo root.
- Dependency management: install from `requirements.txt` into a Python venv before running notebooks.

## Common tasks and explicit commands

- Create an isolated environment and install deps (Windows PowerShell):

  python -m venv .venv; .\.venv\Scripts\Activate.ps1; python -m pip install -r requirements.txt

- Run Jupyter for interactive editing (from repo root):

  jupyter lab

## Project-specific conventions

- Notebooks are the canonical source; small helper scripts or modules are not present. Prefer making minimal, focused edits to cells rather than wholesale reformatting the notebook JSON.
- Preserve existing `metadata.language` and cell `id` fields when editing existing cells. New cells may omit id values.
- Use relative paths for loader inputs (e.g., `TextLoader('speech.txt')`) — tests and CI (if added) will expect relative paths.

## Patterns & examples

- Data ingestion pattern used here:

  1. Instantiate a document loader: `loader = TextLoader('speech.txt')`
  2. Load documents: `text_documents = loader.load()`
  3. Inspect `text_documents` in a notebook cell output

- If adding new Python modules, add them under a top-level package (e.g., `src/`) and update `requirements.txt` if new runtime deps are needed.

## When editing or adding files

- For notebooks: follow the user's notebook format instructions (cells must be valid JSON objects; existing cells must keep `metadata.id`).
- For code files: run a local lint and a quick smoke test by executing the modified notebook cell or a short Python script that imports the module.

## Integration points & external dependencies

- The notebook depends on the `langchain_community` package (used for `TextLoader`) and other packages listed in `requirements.txt`.
- No external services (APIs/DBs) are configured in the repo; if a change requires external credentials, add clear README notes and do not hardcode secrets.

## Testing & validation

- There are no unit tests in the repo. Validate changes by running the notebook cells that exercise the change. When adding code, add a small runnable script or notebook cell that demonstrates the new behavior.

## What not to change

- Avoid changing notebook cell ids for existing cells unless intentionally restructuring the notebook.
- Avoid converting notebooks to scripts unless the user asks — this repo is notebook-first.

## Questions to ask the user before large changes

- Do you want a script/module-based project layout (src/, tests/) or keep it notebook-driven?
- Should I add automated tests or CI? If yes, which test runner and Python versions?

If anything here is unclear or you want more specific conventions (tests, CI, packaging), tell me which direction to take and I will update this file.
