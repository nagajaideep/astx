# ASTx: Abstract Syntax Tree Framework

![CI](https://img.shields.io/github/actions/workflow/status/arxlang/astx/main.yaml?logo=github&label=CI)
[![Python Versions](https://img.shields.io/pypi/pyversions/astx)](https://pypi.org/project/astx/)
[![Package Version](https://img.shields.io/pypi/v/astx?color=blue)](https://pypi.org/project/astx/)
![License](https://img.shields.io/pypi/l/astx?color=blue)
![Discord](https://img.shields.io/discord/966124290464428042?logo=discord&color=blue)

ASTx is a Python library for representing and working with Abstract Syntax Trees
(ASTs). It provides a unified interface for building tools such as compilers,
interpreters, and transpilers.

With ASTx, you can define language constructs, transform ASTs, generate code,
and build tools for analysis.

ASTx is not a lexer or parser. It can be used together with parsers to provide a
higher-level representation of the AST.

It integrates with [IRx](https://github.com/arxlang/irx), enabling code
generation with **LLVM**. Currently, only a subset of ASTx nodes is supported,
but active development is underway.

**Note:** This project is under active development and not ready for production
use.

---

## 🚀 Features

- Language-agnostic: works across different programming languages
- Extensible: add new nodes or extend existing ones
- Code generation: convert ASTs to Python code (other backends planned)
- Includes common constructs: variables, functions, control flow, types
- Initial Symbol Table implementation included

---

## 📦 Installation

Install ASTx from PyPI:

```bash
pip install astx
```

---

## 📖 Overview

ASTx is designed around two main concepts:

1. **Nodes**: each node represents a language construct (e.g., `Variable`,
   `Function`, `IfStmt`)
2. **Tree**: nodes are organized hierarchically, forming an abstract
   representation of the program

ASTx also includes a simple transpiler for converting ASTx nodes to Python code
(text). This feature is for educational purposes, showing how a transpiler can
be implemented.

---

## ✨ Usage

### 1. Create an AST

```python
import astx

# Define a simple function: add(x, y) -> x + y
args = astx.Arguments(
    astx.Argument(name="x", type_=astx.Int32()),
    astx.Argument(name="y", type_=astx.Int32()),
)
fn_body = astx.Block()
fn_body.append(
    astx.FunctionReturn(
        value=astx.BinaryOp(op_code="+", lhs=astx.Variable("x"), rhs=astx.Variable("y"))
    )
)
add_function = astx.FunctionDef(
    prototype=astx.FunctionPrototype(name="add", args=args, return_type=astx.Int32()),
    body=fn_body,
)
```

### 2. Generate Code

Use a transpiler to convert the AST to Python code:

```python
from astx_transpilers.python_string import ASTxPythonTranspiler

transpiler = ASTxPythonTranspiler()
python_code = transpiler.visit(add_function)

print(python_code)
```

Output:

```python
def add(x: int, y: int) -> int:
    return (x + y)
```

### 3. Visualize ASTs

ASTx supports multiple visualization formats:

- YAML
- JSON
- Graphical (PNG or ASCII)

In a Jupyter Notebook, the default visualization is **PNG**. In a console, the
default is **ASCII**.

Example:

```python
print(add_function.to_json())
print(add_function.to_yaml())
```

---

## 🔄 Transpilers

ASTx includes a transpiler system for converting AST structures into Python
code. This can be used for code generation, prototyping, or experimenting with
language tools.

```python
from astx_transpilers.python_string import ASTxPythonTranspiler

transpiler = ASTxPythonTranspiler()
python_code = transpiler.visit(add_function)
print(python_code)
```

**Output:**

```python
def add(x: int, y: int) -> int:
    return (x + y)
```

For more examples, see the
**[transpiler tutorial](docs/tutorials/astx_transpiler_refactor_tutorial.md)**.

---

## 📚 Documentation

Full documentation and examples:
[https://arxlang.github.io/astx](https://arxlang.github.io/astx)

---

## 🛠️ Contributing

Contributions are welcome! See the
[Contributing Guide](https://astx.arxlang.org/contributing/) for details.

---

## 📝 License

ASTx is open-source software licensed under the **BSD-3-Clause License**. See
[LICENSE](LICENSE) for details.
