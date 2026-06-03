# Chapter 7 — Connecting SQL and Python

> Merged notes for **7-1** (Python environment), **7-2** (Python ↔ MySQL), and **7-3** (GUI application).

---

## Part 7-1 — Preparing the Python environment

### Installing Python

Download from [python.org](https://www.python.org/) and install. The bundled **IDLE** editor is enough for these exercises.

### Python essentials used in this chapter

```python
# variables & types
name = "TWICE"; number = 9          # str, int
print(name, number)

# conditional
if number >= 6:
    print("big group")
else:
    print("small group")

# loop
for i in range(1, 4):
    print(i)                          # 1 2 3

# function
def add(a, b):
    return a + b
```

These map closely to SQL programming concepts (Ch 3-3): `if` ↔ `IF`, `for/while` ↔ `WHILE`, `def` ↔ stored function.

---

## Part 7-2 — Linking Python and MySQL

The book uses the **PyMySQL** connector (`pip install PyMySQL`).

### The connection workflow

```
connect()  →  cursor()  →  execute(SQL)  →  [fetch | commit]  →  close()
```

### Inserting data

```python
import pymysql

conn = pymysql.connect(
    host='127.0.0.1', user='root', password='****',
    db='market_db', charset='utf8'
)
cur = conn.cursor()

cur.execute("INSERT INTO member VALUES ('PYT','Python',7,'SE','02','12345678',166,'2022-01-01')")
conn.commit()        # writes (INSERT/UPDATE/DELETE) must be committed
conn.close()
```

### Reading data

```python
conn = pymysql.connect(host='127.0.0.1', user='root', password='****',
                       db='market_db', charset='utf8')
cur = conn.cursor()

cur.execute("SELECT mem_id, mem_name FROM member")
while True:
    row = cur.fetchone()             # one row at a time (or fetchall())
    if row is None:
        break
    print(row[0], row[1])

conn.close()
```

### Parameterized queries (safe input)

Pass values as parameters — **never** build SQL by string concatenation, which invites SQL injection.

```python
cur.execute("SELECT * FROM member WHERE mem_id = %s", (user_input,))
```

| Step | Call | Purpose |
| --- | --- | --- |
| Connect | `pymysql.connect(...)` | open a session |
| Cursor | `conn.cursor()` | object that runs queries |
| Execute | `cur.execute(sql, params)` | send a statement |
| Fetch | `cur.fetchone()` / `fetchall()` | read `SELECT` results |
| Commit | `conn.commit()` | persist writes |
| Close | `conn.close()` | release the connection |

---

## Part 7-3 — A GUI application (tkinter)

`tkinter` is Python's built-in GUI toolkit. Combined with PyMySQL it makes a simple desktop CRUD app.

### Minimal widgets

```python
from tkinter import *

root = Tk()
root.title("Member Manager")

Label(root, text="Member ID:").pack()
entry = Entry(root)
entry.pack()

def on_click():
    print("entered:", entry.get())

Button(root, text="Save", command=on_click).pack()

root.mainloop()      # start the event loop
```

### Wiring the GUI to MySQL

A complete app combines the two: read user input from `Entry` widgets → run an `INSERT`/`SELECT` via PyMySQL → show results in the window. The flow per button click is:

```
read widget values  →  connect  →  execute SQL  →  commit / fetch  →  update the UI  →  close
```

| `tkinter` piece | Role |
| --- | --- |
| `Tk()` | the main window |
| `Label` | static text |
| `Entry` | text input |
| `Button(command=...)` | runs a handler on click |
| `mainloop()` | keeps the window responsive |

---

## Key takeaways

- Python control flow mirrors SQL programming (`if`/`for`/`def` ↔ `IF`/`WHILE`/function).
- PyMySQL flow: **connect → cursor → execute → fetch/commit → close**; always `commit()` after writes.
- Use **parameterized queries** (`%s`), never string-built SQL.
- `tkinter` provides the desktop UI; a real app pairs widget input with PyMySQL calls for full CRUD.
