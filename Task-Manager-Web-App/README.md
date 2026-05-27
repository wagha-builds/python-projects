# Task Manager — Web App

## Description
A lightweight Todo / Task Manager built with **Streamlit**. The application provides a single-page web interface (`web.py`) that renders tasks from a plain text store (`todos.txt`), allows users to add tasks, and marks tasks complete using checkboxes.

The project favors simplicity and transparency. Tasks are stored in a text file and managed through a small helper module, making the code easy to inspect, modify, and extend without introducing unnecessary infrastructure.

Files to review: [web.py](web.py), [functions.py](functions.py), [todos.txt](todos.txt).

---

## Interesting techniques & references

### Streamlit UI primitives
The application uses Streamlit components such as `st.checkbox` and `st.text_input` to bind UI interactions directly to application logic. This allows fast iteration without manual frontend state management.

Streamlit documentation:  
https://docs.streamlit.io

---

### Stateless UI with file-backed persistence
The UI remains reactive while persistence is handled through explicit reads and writes to `todos.txt`. This keeps data flow predictable and easy to reason about.

Python file I/O documentation:  
https://docs.python.org/3/library/io.html

---

### Checkbox-driven completion flow
Tasks are rendered as checkboxes. When a checkbox is selected, the task is removed from the list and the updated state is written back to disk. This keeps interaction logic minimal while maintaining consistency between UI and storage.

---

### Helper module separation
[`functions.py`](functions.py) isolates file read/write logic from presentation logic in [`web.py`](web.py). This structure allows the storage layer to be replaced later without changing the UI code.

---

### Idempotent write strategy
The application rewrites the full contents of `todos.txt` after each update. This avoids partial writes and keeps persistence logic straightforward. In larger systems this approach can be replaced with atomic writes using file replacement.

Python reference:  
https://docs.python.org/3/library/os.html#os.replace

---

### Streamlit reactivity model
The application relies on Streamlit’s rerun model, where UI updates occur automatically after user interaction. Session behavior and state persistence can be extended using Streamlit session state.

Documentation:  
https://docs.streamlit.io/library/advanced-features/session-state

---

## Non-obvious technologies & libraries

### Streamlit
Streamlit serves as both the UI layer and application runtime. It allows Python code to define interactive web interfaces without separate frontend tooling.

- Project page: https://pypi.org/project/streamlit/
- Documentation: https://docs.streamlit.io

---

### Plain-text datastore
The use of a plain text file as the primary datastore is an intentional architectural decision. It removes external dependencies, simplifies debugging, and keeps the application inspectable. The storage layer can later be replaced with JSON, SQLite, or an API-backed service.

---

## External libraries & assets

- **Streamlit** — https://pypi.org/project/streamlit/
- **Python Standard Library** — https://docs.python.org/3/

If additional fonts or static assets are added later, they can be placed under an `assets/` directory and linked here.

---

## Project structure (directories only)

```
/
assets/
docs/
```

### Directory notes
- `assets/`  
  Intended location for images, icons, or static UI resources if added later.

- `docs/`  
  Optional location for extended documentation, design notes, or release information.

Root-level files currently include `web.py`, `functions.py`, `todos.txt`, `requirements.txt`, and this `README.md`.

---

## Files to review

- [`web.py`](web.py) — Streamlit application (UI and interaction flow)
- [`functions.py`](functions.py) — file I/O helper functions
- [`todos.txt`](todos.txt) — plain-text task storage
- [`requirements.txt`](requirements.txt) — project dependencies

---
