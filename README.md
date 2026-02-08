# Task Manager — GUI & CLI

## Description
A minimal task manager that provides two interfaces for the same text-backed to-do list:

- `todolist_project.py` — a small CLI application that reads and writes tasks using helpers from [`functions.py`](functions.py).
- `gui.py` — a desktop GUI built using **FreeSimpleGUI**, displaying tasks in a `Listbox`, updating a live clock, and using an icon (`add.png`) for task creation.

The project demonstrates a pragmatic approach to task management using plain text persistence and a lightweight event-driven GUI. It is intentionally simple and suitable for experimentation, prototyping, and extension into larger systems.

---

## Interesting techniques & references

### Plain-text persistence (readlines / writelines)
The project uses explicit file I/O with `open(..., "r")` and `open(..., "w")` to store tasks in a text file. This keeps persistence transparent and easy to replace with other storage backends later.

Python documentation:  
https://docs.python.org/3/library/io.html

---

### Helper module separation
[`functions.py`](functions.py) isolates file operations from application logic. This separation allows easier testing and makes future storage changes straightforward.

---

### CLI loop with command parsing
`todolist_project.py` uses a simple `while True` loop and command slicing (`add <text>`, `edit <n>`, etc.). This pattern works well for small command-driven tools without introducing external parsers.

---

### Indexed display using `enumerate()`
Tasks are displayed with indices using Python’s built-in `enumerate()` for clarity and simplicity.

Documentation:  
https://docs.python.org/3/library/functions.html#enumerate

---

### Event-driven GUI loop with timeout updates
The GUI uses:

```python
window.read(timeout=200)
```

This allows periodic updates (such as the live clock) without threads. This is a standard event-loop pattern for lightweight GUI applications.

---

### Structural pattern matching (`match` / `case`)
GUI event handling uses Python 3.10+ structural pattern matching instead of chained conditionals.

Documentation:  
https://docs.python.org/3/whatsnew/3.10.html#structural-pattern-matching

---

### Explicit UI update flow
After state changes, the GUI updates the listbox using:

```python
window["todos"].update(values=todos)
```

This demonstrates a clear separation between data mutation and UI refresh without reactive frameworks.

---

### Graceful input error handling
User operations that may fail (invalid indices, incorrect input) are handled using `try/except`, preventing application crashes during normal usage.

---

## Non-obvious technologies & libraries

### FreeSimpleGUI
The GUI layer uses **FreeSimpleGUI**, a continuation of PySimpleGUI that preserves a simple API over traditional GUI backends.

- PyPI: https://pypi.org/project/FreeSimpleGUI/
- Documentation: https://freesimplegui.readthedocs.io/

FreeSimpleGUI acts as a lightweight abstraction over tkinter and other GUI systems, allowing fast UI iteration without large frameworks.

---

### Standard library choices of interest
- `time.strftime` for formatted time display  
  https://docs.python.org/3/library/time.html#time.strftime

- Explicit file I/O (`open`, `readlines`, `writelines`) for predictable persistence behavior.

---

### Python version
The project requires **Python 3.10+** due to the use of structural pattern matching (`match/case`).

---

## External libraries & assets

- FreeSimpleGUI — https://pypi.org/project/FreeSimpleGUI/
- PySimpleGUI (origin project) — https://pysimplegui.readthedocs.io/
- FreeSimpleGUI documentation — https://freesimplegui.readthedocs.io/

### Fonts
The GUI references the system font:

- Helvetica — https://en.wikipedia.org/wiki/Helvetica

Helvetica is typically available on most systems. If portability is required, consider bundling or switching to an alternative font.

---

## Project structure (directories only)

```
/
assets/
docs/
src/
```

### Directory notes
- `assets/`  
  Intended for images and icons referenced by the GUI (for example `add.png`).

- `docs/`  
  Optional location for supporting documentation such as alternative README drafts or notes.

- `src/`  
  Suggested location if the project evolves into a packaged application. Currently, scripts remain at the repository root.

---

## Files to review

- [`functions.py`](functions.py) — file I/O helpers
- [`todolist_project.py`](todolist_project.py) — CLI interface
- [`gui.py`](gui.py) — FreeSimpleGUI desktop interface
- [`todos.txt`](todos.txt) — runtime data file
- [`README1.md`](README1.md)
- [`README2.md`](README2.md)

---
