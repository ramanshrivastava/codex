# Mini-CPython: A Learning-Oriented Python Interpreter

> **A reasoning-based, historically-grounded approach to understanding Python internals by building a simplified interpreter from scratch**

## 🎯 Project Goals

This project is designed for **deep learning** through implementation. By building a mini Python interpreter, you will:

- **Understand** how programming languages work at a fundamental level
- **Learn** lexical analysis, parsing, compilation, and virtual machine execution
- **Discover** Python's design decisions and their historical context
- **Compare** simplified implementations with production CPython code
- **Practice** systems programming in C

## 📊 Project Scope

| Component | Mini-CPython | Real CPython | Purpose |
|-----------|--------------|--------------|---------|
| Total Code | ~6,000-10,000 lines | ~400,000 lines | Learning-focused |
| Tokenizer | 300-500 lines | ~1,600 lines | Lexical analysis |
| Parser | 1,000-2,000 lines | ~1,000+ lines | AST construction |
| Compiler | 1,500-2,000 lines | ~6,500 lines | Bytecode generation |
| VM | 1,500-2,500 lines | ~3,700 lines | Execution engine |
| Objects | 500-1,000 lines | ~30,000 lines | Type system |
| Runtime | 200-500 lines | ~20,000 lines | Memory & lifecycle |

## 🏗️ Architecture

```
Python Source Code
       ↓
  TOKENIZER (Phase 1)    ← Lexical analysis
       ↓
  PARSER (Phase 2)        ← Syntax analysis → AST
       ↓
  COMPILER (Phase 3)      ← Bytecode generation
  ├─ Symbol Table
  ├─ Code Generator
  └─ Assembler
       ↓
  Bytecode
       ↓
  VIRTUAL MACHINE (Phase 4) ← Stack-based execution
       ↓
  Results
```

## 📚 Learning Framework

This project uses a unique **reasoning-based approach**:

### 1. **Architecture Decision Records (ADRs)**
Every design decision is documented with:
- Context: What problem are we solving?
- Decision: What approach did we choose?
- Rationale: Why this over alternatives?
- CPython Reference: How does real CPython do this?
- Historical Context: Python version timeline
- Trade-offs: Benefits and limitations
- Learning Outcomes: What you should understand

### 2. **Historical Timeline**
Each commit maps to Python's evolution:
- Python 0.9.0 (1991) → Basic tokenizer
- Python 1.5 (1997) → Bytecode compiler
- Python 2.5 (2005) → AST introduction (PEP 339)
- Python 3.6 (2016) → Wordcode optimization (PEP 509)

### 3. **Learning Checkpoints**
After each phase:
- Comprehension quiz
- Hands-on exercises
- Debugging challenges
- Comparative analysis
- Performance benchmarks

### 4. **Interactive Tools**
- **Bytecode Visualizer**: See code → bytecode → execution
- **Step-through Debugger**: Inspect VM state
- **Performance Profiler**: Compare with CPython

## 🚀 Getting Started

### Prerequisites
- C compiler (GCC or Clang)
- Make
- Git
- Basic understanding of C programming
- Curiosity about how programming languages work!

### Quick Start

```bash
# Clone and build
cd mini-cpython
make

# Run REPL
./mini-python

# Run a Python file
./mini-python examples/factorial.py

# Visualize bytecode
./tools/visualizer/show_bytecode.py examples/factorial.py
```

## 📖 Learning Path

### **Phase 1: Tokenizer** (Week 1, ~500 lines)
Learn lexical analysis by building a tokenizer
- **Commits**: 1.1-1.4
- **Topics**: Token types, indentation handling, state machines
- **CPython Ref**: `Parser/lexer/lexer.c`
- **Checkpoint**: `docs/checkpoints/phase1-checkpoint.md`

### **Phase 2: Parser** (Week 2, ~1,500 lines)
Learn syntax analysis and AST construction
- **Commits**: 2.1-2.5
- **Topics**: Recursive descent, operator precedence, AST design
- **CPython Ref**: `Parser/pegen.c`, `Python/ast.c`
- **PEPs**: PEP 339 (AST Design)
- **Checkpoint**: `docs/checkpoints/phase2-checkpoint.md`

### **Phase 3: Compiler** (Week 3, ~1,500 lines)
Learn bytecode compilation and code generation
- **Commits**: 3.1-3.4
- **Topics**: Symbol tables, bytecode design, code generation
- **CPython Ref**: `Python/codegen.c`, `Python/symtable.c`
- **PEPs**: PEP 509 (Wordcode)
- **Checkpoint**: `docs/checkpoints/phase3-checkpoint.md`

### **Phase 4: Virtual Machine** (Week 4, ~1,800 lines)
Learn stack-based execution and runtime
- **Commits**: 4.1-4.4
- **Topics**: Stack machines, call frames, control flow
- **CPython Ref**: `Python/ceval.c`
- **Checkpoint**: `docs/checkpoints/phase4-checkpoint.md`

### **Phase 5: Object System** (Week 5, ~1,000 lines)
Learn type systems and object models
- **Commits**: 5.1-5.3
- **Topics**: Type vtables, immutable objects, hash tables
- **CPython Ref**: `Objects/object.c`, `Objects/listobject.c`
- **PEPs**: PEP 253 (Subtyping)
- **Checkpoint**: `docs/checkpoints/phase5-checkpoint.md`

### **Phase 6: Runtime Integration** (Week 6, ~800 lines)
Learn memory management and REPL
- **Commits**: 6.1-6.3
- **Topics**: Reference counting, REPL, error handling
- **CPython Ref**: `Python/pythonrun.c`
- **Checkpoint**: `docs/checkpoints/phase6-checkpoint.md`

## 📁 Project Structure

```
mini-cpython/
├── README.md                    # This file
├── LEARNING_GUIDE.md            # Detailed learning instructions
├── HISTORICAL_TIMELINE.md       # Python evolution & our commits
│
├── docs/
│   ├── adrs/                    # Architecture Decision Records
│   │   ├── 001-tokenizer-design.md
│   │   ├── 002-ast-vs-parse-tree.md
│   │   └── ...
│   ├── comparisons/             # Mini vs Real CPython
│   │   ├── tokenizer-comparison.md
│   │   └── ...
│   ├── checkpoints/             # Learning checkpoints
│   │   ├── phase1-checkpoint.md
│   │   └── ...
│   └── references/              # CPython references & PEPs
│
├── src/
│   ├── lexer/                   # Phase 1: Tokenizer
│   ├── parser/                  # Phase 2: Parser & AST
│   ├── compiler/                # Phase 3: Bytecode compiler
│   ├── vm/                      # Phase 4: Virtual machine
│   ├── objects/                 # Phase 5: Object system
│   └── runtime/                 # Phase 6: Runtime & memory
│
├── tests/
│   ├── unit/                    # Unit tests per component
│   ├── integration/             # End-to-end tests
│   ├── benchmarks/              # Performance tests
│   └── exercises/               # Learning exercises
│
├── examples/                    # Python code to run
│   ├── 01-arithmetic.py
│   ├── 02-variables.py
│   └── ...
│
└── tools/
    ├── visualizer/              # Bytecode visualizer
    ├── debugger/                # Step-through debugger
    └── profiler/                # Performance profiler
```

## 🎓 What You'll Learn

### **Conceptual Understanding**
- ✅ How tokenizers recognize language constructs
- ✅ How parsers build syntax trees
- ✅ How compilers generate bytecode
- ✅ How virtual machines execute code
- ✅ How type systems work
- ✅ How memory management works
- ✅ Why Python makes certain design choices

### **Practical Skills**
- ✅ Reading and understanding large C codebases
- ✅ Implementing data structures (hash tables, stacks)
- ✅ Debugging complex systems
- ✅ Performance analysis and optimization
- ✅ Writing clean, documented C code

### **Historical Context**
- ✅ Python's evolution from 0.9 to 3.13
- ✅ Key PEPs and their rationale
- ✅ Design decisions and trade-offs
- ✅ How CPython became what it is today

## 🔗 Resources

### **CPython Source** (Reference Implementation)
- Location: `/home/user/cpython/`
- Key Files: See `docs/references/cpython-files.md`
- Git: https://github.com/python/cpython

### **Python Enhancement Proposals (PEPs)**
- PEP 339: Design of the Compiler AST
- PEP 509: Add a private version to dict
- PEP 227: Statically Nested Scopes
- Full list: `docs/references/peps-referenced.md`

### **Academic Papers**
- See `docs/references/papers.md`

## 🏆 Success Criteria

By the end of this project, you should be able to:

1. ✅ **Explain** how Python executes code from source to result
2. ✅ **Implement** a new bytecode opcode
3. ✅ **Add** a new built-in type to the object system
4. ✅ **Debug** issues by reading CPython source
5. ✅ **Understand** performance implications of Python features
6. ✅ **Read** and comprehend PEPs and design discussions

## 🤝 Contributing

This is a learning project! Feel free to:
- Suggest improvements to learning materials
- Add more exercises and challenges
- Improve documentation
- Share your learning experience

## 📄 License

MIT License - See LICENSE file

## 🙏 Acknowledgments

- **Guido van Rossum** and the CPython core developers
- **Python Software Foundation**
- All the PEP authors who documented Python's evolution
- The countless tutorials and books on compiler construction

---

**Ready to start learning?** Begin with `LEARNING_GUIDE.md` and then dive into Phase 1!

**Questions?** See the learning checkpoints for FAQs, or explore the ADRs for design rationale.

**Happy Learning! 🚀**
