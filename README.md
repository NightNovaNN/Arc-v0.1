# Arc Utility Language (AUL)

Arc Utility is a lightweight, multi-backend logic DSL (Domain Specific Language) that transpiles into real programming languages such as **C** and **Python**.  
Its goal is to provide a clean, minimal syntax for writing logic, while delegating heavy lifting to established languages.

Arc Utility is **not** designed to replace C or Python —  
instead, it acts as a *portable logic layer* that can generate code across multiple ecosystems.

---

## ✨ Features

### 🟦 Minimal, expressive syntax
```arc
tp C as out.c

x 10
echo x

name "anish"
echo name
````

### 🟩 Multi-language output

```sh
tp C as out.c     # generates out.c
tp Py as out.py   # generates out.py
```

### 🟧 Inline native code

Embed backend-specific code directly:

```arc
inline_c {
#include <stdio.h>
void bruh() {
    printf("BRUH!\n");
}
}
```

When targeting **C**, this block is included untouched.
When targeting **Python**, it is safely commented out.

### 🟨 Smart type inference

Arc Utility automatically chooses the correct C format specifier:

```arc
x 10
name "anish"
echo x      # → printf("%d\n", x)
echo name   # → printf("%s\n", name)
```

### 🟥 Automatic brace fixing

Inline C blocks with missing braces are auto-corrected:

```arc
inline_c {
void f() {
    printf("hi");
}
```

Arc will warn and fix the brace mismatch.

---

## 🚀 Example

### `example.arc`

```arc
tp C as program.c

inline_c {
#include <stdio.h>
}

x 42
echo x

name "Arc Utility"
echo name

inline_c {
void shout() {
    printf("SHOUTING!\n");
}
}
```

### Output (C)

```c
#include <stdio.h>

int x = 42;
printf("%d\n", x);

char* name = "Arc Utility";
printf("%s\n", name);

void shout() {
    printf("SHOUTING!\n");
}
```

---

## 🛠 How It Works

Arc Utility uses a three-stage pipeline:

1. **Parser**
   Reads `.arc` files and converts them into AST nodes.

2. **AST Processing**
   Handles inline blocks, type inference, and validation.

3. **Emitter**
   Generates backend-specific code (C or Python).

The entire compiler is currently ~200 lines of Python.

---

## 📦 Running the Transpiler

```sh
python arc.py yourfile.arc
```

If the file contains:

```arc
tp C as out.c
```

You will get `out.c`.

---

## 🔭 Roadmap

Planned features:

* `if { }` blocks
* `repeat { }` loops
* arithmetic helpers (e.g., `add x 1`)
* JS backend
* C++ backend
* reusable functions (`fn name(args) {}`)
* module system
* VSCode syntax highlighting

---

## 📃 License

MIT License — free to use, modify, and build upon.

---
