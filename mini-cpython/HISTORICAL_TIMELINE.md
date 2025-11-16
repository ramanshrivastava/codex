# Mini-CPython Historical Timeline

> **Mapping our implementation to Python's historical evolution**

## 🕰️ Overview

This document shows how each phase and commit in mini-cpython corresponds to key moments in Python's history. Understanding **why** features were added and **when** helps you appreciate the design decisions.

## 📅 Python Evolution Summary

| Version | Year | Major Changes | Our Phase |
|---------|------|---------------|-----------|
| **Python 0.9.0** | Feb 1991 | First release, basic interpreter | Phase 1 |
| **Python 1.0** | Jan 1994 | Lambda, map, filter, reduce | Phase 2-3 |
| **Python 1.5** | Dec 1997 | Bytecode improvements | Phase 3 |
| **Python 2.0** | Oct 2000 | List comprehensions, GC | Phase 4-5 |
| **Python 2.2** | Dec 2001 | New-style classes, generators | Phase 5 |
| **Python 2.5** | Sep 2006 | AST-based compiler (PEP 339) | Phase 2 |
| **Python 3.0** | Dec 2008 | Major redesign | All Phases |
| **Python 3.6** | Dec 2016 | Wordcode (PEP 509) | Phase 3 |
| **Python 3.11** | Oct 2022 | Faster CPython | Phase 4 |
| **Python 3.13** | Oct 2024 | JIT experiments | Advanced |

---

## Phase 1: Tokenizer (Python 0.9.0 era - 1991)

**Historical Context:**
Guido van Rossum created Python's first tokenizer in 1991. It was inspired by ABC's indentation-based syntax but needed to work with C's standard I/O.

### **Commit 1.1: Basic Tokenizer - Integers & Operators**

**Corresponds to:** Python 0.9.0 (Feb 1991)

**What we implement:**
- Integer literals: `42`, `123`
- Basic operators: `+`, `-`, `*`, `/`
- Parentheses: `(`, `)`
- Newlines and whitespace

**Historical Note:**
Python 0.9.0 had a very simple tokenizer (~200 lines). It could handle:
- Numbers (integers only, no floats initially!)
- Operators
- Simple keywords (if, else, def)

**CPython Reference:**
- Original: Lost to time (1991 code not in Git)
- Modern equivalent: `/home/user/cpython/Parser/lexer/lexer.c:100-300`

**Design Decision:**
We use a simple character-by-character scanner, just like early Python.

**Learning Outcomes:**
- How to recognize tokens with lookahead
- State machine basics
- Why tokenization is separate from parsing

---

### **Commit 1.2: String Literals & Identifiers**

**Corresponds to:** Python 0.9.0 (Feb 1991)

**What we implement:**
- String literals: `"hello"`, `'world'`
- Identifiers: `x`, `variable_name`, `func123`
- Keywords: `if`, `else`, `def`, `return`

**Historical Note:**
Early Python strings were simple - no Unicode, no raw strings, no f-strings. Just basic quoted text.

**CPython Reference:**
- `/home/user/cpython/Parser/lexer/lexer.c:400-600`

**Design Evolution:**
- Python 1.0 (1994): Added raw strings (`r"..."`)
- Python 2.0 (2000): Added Unicode strings (`u"..."`)
- Python 3.0 (2008): All strings became Unicode
- Python 3.6 (2016): Added f-strings (`f"hello {name}"`)

**Learning Outcomes:**
- String escaping challenges
- Keyword vs identifier distinction
- Why Python has multiple string types

---

### **Commit 1.3: Indentation-Based Syntax**

**Corresponds to:** Python 0.9.0 (Feb 1991) - ABC language influence (1980s)

**What we implement:**
- Track indentation levels
- Emit `INDENT` and `DEDENT` tokens
- Stack-based indentation tracking

**Historical Note:**
**This is Python's most distinctive feature!**

Guido was influenced by ABC language (1980s) which used indentation. Other languages (C, Java) use braces `{}`. Python's choice was controversial initially but is now loved.

**Why Indentation?**
1. **Readability** - Forces consistent formatting
2. **Simplicity** - No need for braces
3. **Less typing** - More concise code

**Design Challenge:**
How to represent indentation in tokens?

**CPython's Solution:**
- Maintain a stack of indentation levels
- Emit INDENT when level increases
- Emit multiple DEDENTs when level decreases

**CPython Reference:**
- `/home/user/cpython/Parser/lexer/lexer.c:800-1000`

**Famous Quote:**
> "Python's use of indentation is probably its most controversial feature" - Guido van Rossum, 1993

**Learning Outcomes:**
- Why indentation-based syntax is non-trivial
- Stack-based state tracking
- How one design choice affects the entire language

---

### **Commit 1.4: Error Handling & Line Tracking**

**Corresponds to:** Python 1.0 improvements (1994)

**What we implement:**
- Track line and column numbers
- Report lexical errors with location
- Handle invalid characters gracefully

**Historical Note:**
Early Python error messages were cryptic. Over time, they improved significantly. Python 3.10+ has amazing error messages!

**Evolution of Error Messages:**

**Python 0.9 (1991):**
```
SyntaxError: invalid syntax
```

**Python 3.10+ (2021):**
```
SyntaxError: unmatched ')'
  File "test.py", line 5
    return (x + y))
                  ^
```

**Learning Outcomes:**
- Importance of good error messages
- Source location tracking
- Error recovery strategies

---

## Phase 2: Parser (Python 2.5 era - 2006)

**Historical Context:**
Python used different parsing techniques over time:
- **1991-2005**: LL(1) parser generator
- **2006-2020**: AST-based compiler (PEP 339)
- **2020+**: PEG parser (PEP 617)

### **Commit 2.1: AST Node Definitions**

**Corresponds to:** Python 2.5 (Sep 2006) - PEP 339

**What we implement:**
- AST node structures
- Module, Statement, Expression types
- Type-safe node creation

**Historical Note:**
**PEP 339 (2005) was a major milestone!**

Before: Python compiled directly from parse tree
After: Python uses AST as intermediate representation

**Why the change?**
1. **Separation of concerns** - Parsing vs compilation
2. **Easier optimization** - Transform AST before codegen
3. **Better tooling** - External tools can use AST

**PEP 339 Quote:**
> "The current bytecode compiler converts the parse tree directly to bytecode. This design has several disadvantages... An AST would make it easier to write code analysis tools"

**CPython Reference:**
- `/home/user/cpython/Parser/Python.asdl` - AST definition
- `/home/user/cpython/Python/ast.c` - AST construction

**Learning Outcomes:**
- AST vs parse tree trade-offs
- Why intermediate representations matter
- How to design tree structures

---

### **Commit 2.2: Expression Parser**

**Corresponds to:** Python 0.9.0 expressions (1991)

**What we implement:**
- Binary operations: `1 + 2 * 3`
- Operator precedence: `*` before `+`
- Unary operations: `-x`, `not x`
- Parenthesized expressions: `(1 + 2) * 3`

**Historical Note:**
Python's operator precedence matches mathematical conventions:
1. Parentheses `()`
2. Exponentiation `**`
3. Unary `+`, `-`, `~`, `not`
4. Multiply/Divide `*`, `/`, `//`, `%`
5. Add/Subtract `+`, `-`
6. Comparisons `<`, `>`, `==`, etc.
7. Boolean `and`, `or`

**Parsing Technique Evolution:**
- **Early Python**: Precedence table in parser generator
- **Our approach**: Precedence climbing (Pratt parsing)
- **Modern CPython**: PEG grammar

**CPython Reference:**
- `/home/user/cpython/Grammar/python.gram` - Grammar rules
- `/home/user/cpython/Parser/parser.c` - Generated parser

**Learning Outcomes:**
- Operator precedence implementation
- Recursive descent parsing
- Left vs right associativity

---

### **Commit 2.3: Statement Parser**

**Corresponds to:** Python 1.0 (1994)

**What we implement:**
- Assignments: `x = 42`
- Print/Expression statements: `print(x)`
- Return statements: `return x + y`

**Historical Note:**
Python 2.x had `print` as a statement:
```python
print "hello"  # Python 2
```

Python 3.0 made it a function:
```python
print("hello")  # Python 3
```

**Why the change? (PEP 3105)**
1. Consistency - everything is an expression
2. Flexibility - can override print behavior
3. Compatibility - easier to support both

**Learning Outcomes:**
- Statement vs expression distinction
- Language evolution and backward compatibility
- Design consistency

---

### **Commit 2.4: Control Flow Parsing**

**Corresponds to:** Python 0.9.0 (1991)

**What we implement:**
- If/else: `if x > 0: ... else: ...`
- While loops: `while condition: ...`
- For loops: `for x in range(10): ...`

**Historical Note:**
Python initially had:
- `if`/`elif`/`else`
- `while`
- `for`... but only for sequences!

**For Loop Evolution:**

**Python 1.0 (1994):** Only lists
```python
for x in [1, 2, 3]:
    print(x)
```

**Python 2.2 (2001):** Iterators (PEP 234)
```python
for x in range(1000000):  # Memory efficient!
    print(x)
```

**Design Insight:**
Python's `for` is actually "for each" - it always iterates over a sequence/iterator. No C-style `for(i=0; i<10; i++)`.

**Learning Outcomes:**
- Different loop models (for-each vs for-index)
- How syntax reflects semantics
- Iterator protocol design

---

### **Commit 2.5: Function Definitions**

**Corresponds to:** Python 0.9.0 (1991)

**What we implement:**
- Function definitions: `def foo(a, b): ...`
- Parameters and arguments
- Return statements

**Historical Note:**

**Python 0.9 (1991):** Basic functions
```python
def add(a, b):
    return a + b
```

**Python 1.0 (1994):** Default arguments
```python
def greet(name="World"):
    return "Hello, " + name
```

**Python 2.0 (2000):** `*args`, `**kwargs`
```python
def func(*args, **kwargs):
    pass
```

**Python 3.0 (2008):** Keyword-only args (PEP 3102)
```python
def func(a, b, *, c, d):  # c and d must be named
    pass
```

**Learning Outcomes:**
- Function as first-class objects
- Argument passing mechanisms
- Scope introduction

---

## Phase 3: Compiler (Python 1.5-3.6 era)

**Historical Context:**
Python's bytecode format evolved significantly:
- **1994**: Basic stack machine
- **1997**: Optimized bytecode (Python 1.5)
- **2006**: AST-based compiler (Python 2.5)
- **2016**: Wordcode (Python 3.6, PEP 509)

### **Commit 3.1: Symbol Table Construction**

**Corresponds to:** Python 2.1 (2001) - PEP 227 (Nested Scopes)

**What we implement:**
- Scope analysis (local/global)
- Symbol table per scope
- Detect undefined variables

**Historical Note:**
**PEP 227 (2000) - Statically Nested Scopes**

Before Python 2.1, closures didn't work properly:

**Python 2.0 (broken):**
```python
def outer():
    x = 10
    def inner():
        return x  # ERROR! x not found
    return inner
```

**Python 2.1+ (works):**
```python
def outer():
    x = 10
    def inner():
        return x  # OK! x from enclosing scope
    return inner
```

**Design Change:**
- Added FREE variables (from enclosing scope)
- Required static scope analysis
- Symbol table construction became essential

**CPython Reference:**
- `/home/user/cpython/Python/symtable.c` (3,246 lines!)

**Learning Outcomes:**
- Static vs dynamic scoping
- Closure implementation requirements
- Why symbol tables are non-trivial

---

### **Commit 3.2: Bytecode Instruction Set**

**Corresponds to:** Python 3.6 (2016) - PEP 509 (Wordcode)

**What we implement:**
- 30 essential opcodes
- 1-byte opcode + 1-byte argument format
- Stack-based instruction set

**Historical Note:**
**PEP 509 (2016) - Add a private version to dict**

Actually about **wordcode** format:

**Before Python 3.6:** Variable-length bytecode
- Some instructions: 1 byte
- Some instructions: 3 bytes
- Required complex decoding

**Python 3.6+:** Fixed-width "wordcode"
- Every instruction: 2 bytes
- Simpler, faster decoding
- Better cache locality

**Format:**
```
[OPCODE][ARG][OPCODE][ARG][OPCODE][ARG]...
  byte    byte  byte    byte  byte    byte
```

**CPython Reference:**
- `/home/user/cpython/Include/opcode.h` - Opcode definitions
- `/home/user/cpython/Python/codegen.c` - Code generation

**Opcode Count Evolution:**
- Python 1.0: ~60 opcodes
- Python 2.7: ~100 opcodes
- Python 3.13: ~250+ opcodes (with specialization)

**Our Approach:**
We implement ~30 essential opcodes, enough for:
- Arithmetic
- Variables
- Control flow
- Functions
- Basic data structures

**Learning Outcomes:**
- Instruction set design
- Stack machine vs register machine
- Trade-offs in bytecode format

---

### **Commit 3.3: Expression Code Generation**

**Corresponds to:** Python 1.0 (1994)

**What we implement:**
- Compile expressions to bytecode
- Constant folding (simple optimization)
- Stack depth calculation

**Historical Note:**

**Constant Folding** has been in Python since early days:

```python
# Source code
x = 2 + 3 * 4

# Without optimization
LOAD_CONST 2
LOAD_CONST 3
LOAD_CONST 4
BINARY_MULTIPLY
BINARY_ADD
STORE_FAST x

# With constant folding (since Python 2.1)
LOAD_CONST 14    # 2 + 3*4 = 14 (computed at compile time!)
STORE_FAST x
```

**Optimization Evolution:**
- Python 1.x: No optimization
- Python 2.1: Constant folding
- Python 2.3: Peephole optimizer
- Python 3.6+: Aggressive inlining
- Python 3.11+: Specialization, JIT hints

**CPython Reference:**
- `/home/user/cpython/Python/codegen.c:500-2000`

**Learning Outcomes:**
- When to optimize (compile time vs runtime)
- AST transformations
- Stack depth tracking importance

---

### **Commit 3.4: Control Flow Compilation**

**Corresponds to:** Python 1.0 (1994)

**What we implement:**
- Jump instructions (forward/backward)
- Jump patching (fix addresses later)
- Basic blocks

**Historical Note:**

**Jump Patching Challenge:**

When compiling `if`, you don't know the else block's address yet:

```python
if condition:    # Compile this first
    block1       # Don't know where "else" is yet!
else:
    block2
```

**Solution:** Forward references and patching
1. Emit jump with placeholder address
2. Remember jump location
3. Come back and patch it later

**CPython's Approach:**
Uses a flowgraph with basic blocks, then assembles.

**Our Approach:**
Simple list of instructions with jump patching.

**Learning Outcomes:**
- Forward references in compilation
- Why assembly has multiple passes
- Basic blocks and control flow graphs

---

## Phase 4: Virtual Machine (Python 1.0-3.11 era)

**Historical Context:**
Python's VM evolved from simple interpreter to highly optimized execution engine:
- **1991**: Basic interpreter
- **1994**: Stack-based VM established
- **2001**: Generators (PEP 255)
- **2022**: Specialized opcodes (Python 3.11)

### **Commit 4.1: Stack Machine Implementation**

**Corresponds to:** Python 1.0 (1994)

**What we implement:**
- Value stack
- Opcode dispatch loop
- Arithmetic operations

**Historical Note:**

**Why Stack-Based?**

Python uses a **stack machine** not a **register machine**.

**Stack Machine:**
```
LOAD_CONST 2      # Stack: [2]
LOAD_CONST 3      # Stack: [2, 3]
BINARY_ADD        # Stack: [5]
```

**Register Machine (like Lua):**
```
LOAD R1, 2
LOAD R2, 3
ADD R3, R1, R2
```

**Trade-offs:**

| Aspect | Stack Machine | Register Machine |
|--------|--------------|------------------|
| Code size | Smaller | Larger |
| Decode | Simpler | More complex |
| Performance | Slower | Faster |
| Implementation | Easier | Harder |

**Python chose stack** for simplicity and portability (1991 decision).

**CPython Reference:**
- `/home/user/cpython/Python/ceval.c:1500-2500`

**Learning Outcomes:**
- Stack vs register machines
- Opcode dispatch techniques
- Why Python is "slow" (bytecode interpretation overhead)

---

### **Commit 4.2: Variables & Namespaces**

**Corresponds to:** Python 1.0 (1994)

**What we implement:**
- Local variables (fast locals)
- Global variables (dict-based)
- LOAD_FAST, STORE_FAST, LOAD_GLOBAL, STORE_GLOBAL

**Historical Note:**

**Python's Namespace Model:**

Everything in Python is a dictionary!

**Locals (fast path):**
```python
def func():
    x = 10  # STORE_FAST 0 (array lookup - fast!)
    return x
```

**Globals (slow path):**
```python
global_var = 10  # Stored in module.__dict__ (hash table - slower)
```

**Why Different?**
- Locals: Known at compile time → use array
- Globals: Dynamic (can add/delete at runtime) → use dict

**Evolution:**
- Python 1.0: locals() returned a dict
- Python 3.11+: locals() still returns dict, but internal representation is array

**CPython Reference:**
- `/home/user/cpython/Python/ceval.c:2500-3000`

**Learning Outcomes:**
- Fast path vs slow path optimization
- When static analysis helps performance
- Trade-offs in dynamic languages

---

### **Commit 4.3: Control Flow Execution**

**Corresponds to:** Python 1.0 (1994)

**What we implement:**
- JUMP_FORWARD, JUMP_ABSOLUTE
- POP_JUMP_IF_FALSE, POP_JUMP_IF_TRUE
- Loop execution

**Historical Note:**

**Computed Gotos (CPython Optimization):**

CPython uses GCC's "computed goto" extension for faster dispatch:

**Normal switch (slower):**
```c
switch (opcode) {
    case BINARY_ADD:
        // handle
        break;
    case LOAD_CONST:
        // handle
        break;
}
```

**Computed goto (faster):**
```c
static void *dispatch_table[] = {
    &&BINARY_ADD,
    &&LOAD_CONST,
    // ...
};

DISPATCH();  // goto *dispatch_table[opcode]
```

**Performance Gain:** ~15-20% faster!

**Our Approach:** Simple switch (portable, easier to understand)

**CPython Reference:**
- `/home/user/cpython/Python/ceval.c:1000-1500`

**Learning Outcomes:**
- Dispatch optimization techniques
- Portability vs performance trade-offs
- How interpreters achieve speed

---

### **Commit 4.4: Function Calls & Frames**

**Corresponds to:** Python 1.0 (1994) - Python 2.3 (generators)

**What we implement:**
- Call frames (stack frames)
- Function call protocol
- Return value handling
- Recursion limit

**Historical Note:**

**Frame Objects:**

Each function call creates a frame:

```python
def a():
    b()

def b():
    c()

def c():
    pass  # At this point: 3 frames on call stack
```

**Frame contains:**
- Code object (bytecode)
- Local variables
- Value stack
- Program counter (instruction pointer)
- Back pointer (previous frame)

**Recursion Limit:**

Python has a default recursion limit (1000 calls):

```python
>>> def recurse():
...     recurse()
>>> recurse()
RecursionError: maximum recursion depth exceeded
```

**Why?**
Prevent stack overflow in C interpreter.

**CPython Reference:**
- `/home/user/cpython/Python/ceval.c:4500-6000`
- `/home/user/cpython/Objects/frameobject.c`

**Learning Outcomes:**
- Call stack implementation
- Why recursion limits exist
- Frame objects and introspection

---

## Phase 5: Object System (Python 2.2-3.0 era)

**Historical Context:**
Python's object model evolved significantly:
- **0.9.0 (1991)**: Simple types
- **2.0 (2000)**: Integers/longs merged
- **2.2 (2001)**: New-style classes (PEP 252/253)
- **3.0 (2008)**: Everything is an object

### **Commit 5.1: Base Object & Type System**

**Corresponds to:** Python 2.2 (2001) - PEP 252 & 253

**What we implement:**
- PyObject base structure
- PyType type structure
- Reference counting

**Historical Note:**

**PEP 252 & 253 (2001) - Type/Class Unification**

**Before Python 2.2:**
- Built-in types (list, dict) != User classes
- Can't subclass list!
- Type and class are different

**Python 2.2+:**
- Everything inherits from `object`
- Can subclass built-in types
- `type` and `class` unified

```python
# Python 2.2+
class MyList(list):  # Can subclass built-in!
    pass
```

**Type Hierarchy:**
```
object (base of everything)
  ├── type (metaclass)
  ├── int
  ├── str
  ├── list
  └── ... all types
```

**CPython Reference:**
- `/home/user/cpython/Objects/object.c`
- `/home/user/cpython/Include/object.h`

**Learning Outcomes:**
- Object model design
- Type systems and vtables
- Why "everything is an object" matters

---

### **Commit 5.2: Integer & String Objects**

**Corresponds to:** Python 3.0 (2008) - Integer/Long unification

**What we implement:**
- PyIntObject (arbitrary precision)
- PyStrObject (Unicode strings)
- Immutable object semantics

**Historical Note:**

**Integer Evolution:**

**Python 2.x:** Two types
- `int`: 32/64-bit
- `long`: Arbitrary precision

```python
>>> 2**31 - 1      # int
2147483647
>>> 2**31          # automatically becomes long!
2147483648L
```

**Python 3.0+:** Only `int`
- Always arbitrary precision
- No more `long` type

**String Evolution:**

**Python 2.x:** Two types
- `str`: Bytes
- `unicode`: Unicode

**Python 3.0+:** One type
- `str`: Unicode
- `bytes`: Bytes

**CPython Reference:**
- `/home/user/cpython/Objects/longobject.c` - Arbitrary precision
- `/home/user/cpython/Objects/unicodeobject.c` - Unicode

**Learning Outcomes:**
- Arbitrary precision arithmetic
- Unicode handling complexity
- Immutable vs mutable objects

---

### **Commit 5.3: List & Dict Objects**

**Corresponds to:** Python 1.0 (lists), Python 3.6 (ordered dicts)

**What we implement:**
- PyListObject (dynamic array)
- PyDictObject (hash table)
- Mutable object semantics

**Historical Note:**

**Dictionary Evolution:**

**Python 1.0-3.5:** Unordered
```python
>>> d = {'a': 1, 'b': 2, 'c': 3}
>>> d.keys()
['c', 'a', 'b']  # Random order!
```

**Python 3.6:** Ordered (implementation detail)

**Python 3.7+:** Ordered (guaranteed)
```python
>>> d = {'a': 1, 'b': 2, 'c': 3}
>>> d.keys()
['a', 'b', 'c']  # Insertion order preserved!
```

**Why the change?**
- Memory efficiency (compact representation)
- Better cache locality
- Side effect: preserved insertion order!

**Hash Table Design:**

Python uses open addressing (not chaining):
```
Hash: [Entry][Entry][ None ][Entry]...
```

**Collision Resolution:**
- Probe sequence (perturbed random walk)
- Resize when 2/3 full

**CPython Reference:**
- `/home/user/cpython/Objects/dictobject.c` (7,776 lines!)
- `/home/user/cpython/Objects/listnotes.txt`

**Learning Outcomes:**
- Hash table implementation
- Dynamic array resizing
- Why dicts are fast

---

## Phase 6: Runtime Integration (Python 1.0-2.0 era)

**Historical Context:**
Memory management evolved:
- **1.0 (1994)**: Reference counting only
- **2.0 (2000)**: Cycle-detecting GC (PEP 222)
- **3.4 (2014)**: Improved GC

### **Commit 6.1: Reference Counting**

**Corresponds to:** Python 1.0 (1994)

**What we implement:**
- INCREF/DECREF macros
- Reference count tracking
- Object deallocation

**Historical Note:**

**Why Reference Counting?**

Python uses **reference counting** not **tracing GC** (like Java/Go).

**Advantages:**
- Deterministic cleanup (objects freed immediately)
- Simple implementation
- Works well with C extensions

**Disadvantages:**
- Cannot handle cycles:
```python
a = []
b = []
a.append(b)  # a → b
b.append(a)  # b → a (cycle!)
# Neither will ever be freed!
```

**Solution:** Cycle detector added in Python 2.0

**CPython Reference:**
- `/home/user/cpython/Objects/object.c:200-400`

**Learning Outcomes:**
- Reference counting mechanics
- Memory leaks in refcounting
- Why cycles are problematic

---

### **Commit 6.2: REPL Implementation**

**Corresponds to:** Python 1.0 (1994)

**What we implement:**
- Read-Eval-Print-Loop
- Interactive mode
- Multi-line input handling

**Historical Note:**

**Interactive Python:**

```
>>> 2 + 2
4
>>> def fact(n):
...     if n <= 1: return 1
...     return n * fact(n-1)
...
>>> fact(5)
120
```

**Challenges:**
- Incomplete input detection (need more lines?)
- State management (variables persist)
- Error recovery (don't crash on syntax error)

**CPython Reference:**
- `/home/user/cpython/Python/pythonrun.c`

**Learning Outcomes:**
- REPL architecture
- Interactive interpreter challenges
- State management

---

### **Commit 6.3: Error Handling & Traceback**

**Corresponds to:** Python 1.0-3.10 evolution

**What we implement:**
- Exception propagation
- Stack traceback
- Error messages

**Historical Note:**

**Exception Evolution:**

**Python 1.0 (1994):** Basic exceptions
```
Traceback (innermost last):
  File "<stdin>", line 1
ZeroDivisionError: integer division or modulo
```

**Python 3.10+ (2021):** Enhanced error messages!
```
Traceback (most recent call last):
  File "test.py", line 5, in <module>
    result = divide(10, 0)
             ^^^^^^^^^^^^^^
  File "test.py", line 2, in divide
    return a / b
           ~~^~~
ZeroDivisionError: division by zero
```

**PEP 657 (2021):** Fine-grained error locations

**Learning Outcomes:**
- Exception propagation
- Traceback construction
- User experience in error reporting

---

## 🎯 Summary: Our Journey Through Python History

| Our Phase | Python Era | Key Innovation | Year |
|-----------|------------|----------------|------|
| Phase 1 | Python 0.9.0 | Indentation-based syntax | 1991 |
| Phase 2 | Python 2.5 | AST-based compiler | 2006 |
| Phase 3 | Python 3.6 | Wordcode bytecode | 2016 |
| Phase 4 | Python 1.0-3.11 | Stack VM + optimizations | 1994-2022 |
| Phase 5 | Python 2.2-3.0 | Object model unification | 2001-2008 |
| Phase 6 | Python 1.0-2.0 | Refcounting + GC | 1994-2000 |

## 📚 Key PEPs Referenced

- **PEP 227** (2000): Statically Nested Scopes
- **PEP 255** (2001): Simple Generators
- **PEP 339** (2005): Design of the Compiler AST
- **PEP 509** (2016): Add a private version to dict (Wordcode)
- **PEP 252/253** (2001): Type/Class Unification
- **PEP 3102** (2007): Keyword-Only Arguments
- **PEP 3105** (2007): Make print a function
- **PEP 617** (2020): New PEG parser

Full list: `docs/references/peps-referenced.md`

---

**Next Steps:**
1. Review this timeline
2. Read `LEARNING_GUIDE.md`
3. Start Phase 1, Commit 1.1!

**Remember:** We're not just building an interpreter. We're tracing 30+ years of Python's evolution! 🐍
