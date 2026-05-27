# 🖥️ Task Manager GUI App

This is a simple **Task Manager (To-Do List)** desktop application built using **Python** and **FreeSimpleGUI**.  
It helps you manage, edit, and complete tasks through an intuitive graphical interface.

---

## 📖 Description

The GUI version of the Task Manager allows users to:
- Add new tasks
- Edit existing tasks
- Mark tasks as completed
- View real-time clock updates
- Exit safely through a button interface

All tasks are stored in a text file (`todos.txt`), allowing data persistence between sessions.

---

## 📂 Files Used

### **gui.py**
This is the main file that runs the graphical user interface of the Task Manager.

**Key Features:**
- Built using **FreeSimpleGUI** with a modern `DarkTeal12` theme.
- Displays the current date and time dynamically.
- Allows adding, editing, completing, and viewing todos.
- Uses event-driven programming via `window.read()` loop.


        case "todos":
            window["todo"].update(value=values['todos'][0])
        case sg.WIN_CLOSED:
            break
