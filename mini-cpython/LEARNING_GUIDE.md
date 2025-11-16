# Mini-CPython Learning Guide

> **How to use this project for maximum learning impact**

## 🎯 Learning Philosophy

This project is designed around **active learning through implementation**. You learn best by:

1. **Reading** CPython source code to understand real-world implementations
2. **Implementing** simplified versions to grasp core concepts
3. **Comparing** your implementation with CPython to see trade-offs
4. **Testing** your understanding through exercises and challenges
5. **Reflecting** on design decisions through ADRs and checkpoints

## 📖 How to Use This Project

### **Step 1: Read the Roadmap**

Start with `HISTORICAL_TIMELINE.md` to understand:
- What you'll build in each phase
- How it maps to Python's historical evolution
- What CPython files you'll reference
- What PEPs explain the design decisions

### **Step 2: Study Before Implementing**

For each phase (e.g., Phase 1: Tokenizer):

1. **Read the ADR** for that phase
   - Example: `docs/adrs/001-tokenizer-design.md`
   - Understand the problem and design space

2. **Study CPython Source**
   - Location: `/home/user/cpython/Parser/lexer/lexer.c`
   - Focus on the concepts, not every detail
   - Use the comparison doc: `docs/comparisons/tokenizer-comparison.md`

3. **Review Historical Context**
   - Read referenced PEPs
   - Understand why Python evolved this way

### **Step 3: Implement Incrementally**

Follow the commits in order:

```bash
# Checkout the starting point for Phase 1.1
git checkout phase-1.1-start

# Read the commit message for context
git log -1 --format=full

# Implement the feature described
# ...

# Compare with the reference implementation
git checkout phase-1.1-complete
git diff phase-1.1-start phase-1.1-complete
```

**Each commit includes:**
- Working code
- Unit tests
- Updated ADR
- Documentation

### **Step 4: Test Your Understanding**

After implementing each phase:

1. **Run the checkpoint quiz**
   - Example: `docs/checkpoints/phase1-checkpoint.md`
   - Answer questions without looking at code

2. **Complete exercises**
   - Extend features
   - Fix intentional bugs
   - Optimize performance

3. **Read CPython again**
   - Now that you've implemented it, re-read CPython
   - You'll understand much more the second time!

### **Step 5: Reflect and Document**

- Write your own notes on what you learned
- Compare your first attempt with the reference
- Document your "aha!" moments

## 🔍 Study Techniques

### **1. Side-by-Side Comparison**

Always have three windows open:

```
┌─────────────────────┬─────────────────────┬─────────────────────┐
│  Your Code          │  CPython Source     │  ADR/Documentation  │
│  mini-cpython/src/  │  /home/user/cpython/│  docs/adrs/         │
└─────────────────────┴─────────────────────┴─────────────────────┘
```

### **2. Trace Execution**

Use the debugger to step through:

```bash
# Your implementation
./tools/debugger/step.py examples/factorial.py

# Watch the stack, frame, and bytecode execution
```

### **3. Visualize Data Flow**

```bash
# See the full pipeline
./tools/visualizer/show_bytecode.py examples/fibonacci.py

# Output shows:
# 1. Source code
# 2. Tokens
# 3. AST
# 4. Bytecode
# 5. Execution trace
```

### **4. Benchmark and Profile**

```bash
# Compare performance
./tools/profiler/compare.py examples/loops.py

# Understand why CPython is faster
# Learn optimization techniques
```

## 📚 Learning by Phase

### **Phase 1: Tokenizer**

**Before implementing:**
- [ ] Read `docs/adrs/001-tokenizer-design.md`
- [ ] Study `/home/user/cpython/Parser/lexer/lexer.c`
- [ ] Read about state machines and lexical analysis
- [ ] Understand Python's indentation-based syntax

**While implementing:**
- [ ] Start with Commit 1.1 (integers & operators)
- [ ] Write unit tests first
- [ ] Compare output with Python's `tokenize` module
- [ ] Test edge cases (nested indentation, errors)

**After implementing:**
- [ ] Complete `docs/checkpoints/phase1-checkpoint.md`
- [ ] Try exercises: add new token types
- [ ] Read CPython lexer again with new understanding
- [ ] Write reflection notes

**Key Learning Outcomes:**
- How lexical analysis works
- State machine design
- Handling indentation-sensitive syntax
- Error recovery strategies

### **Phase 2: Parser**

**Before implementing:**
- [ ] Read `docs/adrs/005-ast-design.md`
- [ ] Study `/home/user/cpython/Python/ast.c`
- [ ] Read PEP 339 (AST Design)
- [ ] Learn about recursive descent parsing

**While implementing:**
- [ ] Understand operator precedence
- [ ] Implement expression parsing first
- [ ] Then add statement parsing
- [ ] Finally add control flow

**After implementing:**
- [ ] Complete `docs/checkpoints/phase2-checkpoint.md`
- [ ] Visualize AST for complex expressions
- [ ] Add a new statement type (exercise)
- [ ] Compare with Python's `ast` module output

**Key Learning Outcomes:**
- AST vs parse tree
- Recursive descent parsing
- Operator precedence handling
- Python's grammar structure

### **Phase 3: Compiler**

**Before implementing:**
- [ ] Read `docs/adrs/010-symbol-table.md`
- [ ] Study `/home/user/cpython/Python/codegen.c`
- [ ] Read PEP 227 (Nested Scopes)
- [ ] Understand bytecode instruction sets

**While implementing:**
- [ ] Start with symbol table analysis
- [ ] Design your bytecode instruction set
- [ ] Implement code generation for expressions
- [ ] Add control flow compilation (jumps)

**After implementing:**
- [ ] Complete `docs/checkpoints/phase3-checkpoint.md`
- [ ] Disassemble bytecode by hand
- [ ] Compare with Python's `dis` module
- [ ] Implement constant folding (optimization)

**Key Learning Outcomes:**
- Symbol table construction
- Bytecode design trade-offs
- Code generation patterns
- Basic optimizations

### **Phase 4: Virtual Machine**

**Before implementing:**
- [ ] Read `docs/adrs/014-stack-machine.md`
- [ ] Study `/home/user/cpython/Python/ceval.c`
- [ ] Understand stack-based VMs
- [ ] Learn about call frames and scope

**While implementing:**
- [ ] Build the stack machine first
- [ ] Add variable storage (locals/globals)
- [ ] Implement control flow (jumps)
- [ ] Add function calls and returns

**After implementing:**
- [ ] Complete `docs/checkpoints/phase4-checkpoint.md`
- [ ] Trace execution by hand
- [ ] Implement tail call optimization
- [ ] Profile performance bottlenecks

**Key Learning Outcomes:**
- Stack machine execution model
- Call frame management
- Scope and namespace handling
- VM optimization techniques

### **Phase 5: Object System**

**Before implementing:**
- [ ] Read `docs/adrs/018-object-model.md`
- [ ] Study `/home/user/cpython/Objects/object.c`
- [ ] Read PEP 253 (Subtyping)
- [ ] Understand vtables and dispatch

**While implementing:**
- [ ] Define base object structure
- [ ] Implement type system
- [ ] Add built-in types (int, str, list, dict)
- [ ] Implement operations via vtables

**After implementing:**
- [ ] Complete `docs/checkpoints/phase5-checkpoint.md`
- [ ] Implement your own custom type
- [ ] Study hash table implementation
- [ ] Understand method resolution order

**Key Learning Outcomes:**
- Object model design
- Type system implementation
- Polymorphism via vtables
- Data structure internals

### **Phase 6: Runtime Integration**

**Before implementing:**
- [ ] Read `docs/adrs/021-memory-management.md`
- [ ] Study `/home/user/cpython/Python/pythonrun.c`
- [ ] Understand reference counting
- [ ] Learn about REPL implementation

**While implementing:**
- [ ] Add reference counting
- [ ] Implement REPL loop
- [ ] Add error handling and exceptions
- [ ] Build final integration

**After implementing:**
- [ ] Complete `docs/checkpoints/phase6-checkpoint.md`
- [ ] Run real Python programs
- [ ] Find and fix memory leaks
- [ ] Add garbage collection (bonus)

**Key Learning Outcomes:**
- Memory management strategies
- REPL state management
- Exception propagation
- System integration

## 🎯 Learning Objectives

### **Level 1: Understanding (Week 1-2)**
After Phase 1-2, you should be able to:
- [ ] Explain how Python tokenizes source code
- [ ] Describe the AST structure
- [ ] Identify tokens and AST nodes for given code
- [ ] Understand basic parsing techniques

### **Level 2: Application (Week 3-4)**
After Phase 3-4, you should be able to:
- [ ] Generate bytecode for Python code
- [ ] Trace bytecode execution by hand
- [ ] Implement new opcodes
- [ ] Debug bytecode issues

### **Level 3: Analysis (Week 5-6)**
After Phase 5-6, you should be able to:
- [ ] Compare implementation strategies
- [ ] Analyze performance trade-offs
- [ ] Identify optimization opportunities
- [ ] Understand CPython design decisions

### **Level 4: Mastery (Beyond)**
After completing all phases, you should be able to:
- [ ] Read CPython source fluently
- [ ] Contribute to CPython discussions
- [ ] Design language features
- [ ] Implement your own language

## 🧪 Exercises and Challenges

### **Type A: Extension Exercises**
Implement new features to deepen understanding:

**Phase 1 Extensions:**
- [ ] Add support for f-strings
- [ ] Handle Unicode identifiers
- [ ] Implement raw strings (r"...")

**Phase 2 Extensions:**
- [ ] Add list comprehensions
- [ ] Implement lambda expressions
- [ ] Support generator expressions

**Phase 3 Extensions:**
- [ ] Implement constant folding optimization
- [ ] Add dead code elimination
- [ ] Support inline caching

**Phase 4 Extensions:**
- [ ] Implement tail call optimization
- [ ] Add tracing/debugging hooks
- [ ] Support coroutines

**Phase 5 Extensions:**
- [ ] Implement classes and inheritance
- [ ] Add operator overloading
- [ ] Support descriptors

**Phase 6 Extensions:**
- [ ] Implement cycle-detecting GC
- [ ] Add module import system
- [ ] Support multi-threading

### **Type B: Debugging Challenges**
Fix intentional bugs to practice debugging:

Each checkpoint includes 3-5 buggy programs:
- [ ] Memory leak in object allocation
- [ ] Off-by-one error in bytecode jump
- [ ] Incorrect operator precedence
- [ ] Stack corruption in function calls
- [ ] Reference counting bug

### **Type C: Performance Challenges**
Optimize code to understand trade-offs:

- [ ] Profile a slow program
- [ ] Identify bottleneck
- [ ] Implement optimization
- [ ] Measure improvement
- [ ] Compare with CPython approach

### **Type D: Reading Challenges**
Read CPython code to understand real implementations:

- [ ] Trace CPython's execution of a program
- [ ] Find where a specific feature is implemented
- [ ] Understand a complex optimization
- [ ] Read a related PEP
- [ ] Explain implementation to someone else

## 📊 Progress Tracking

### **Self-Assessment Checklist**

After each phase, rate yourself (1-5):

**Understanding:**
- [ ] I can explain the concepts clearly
- [ ] I understand the design decisions
- [ ] I can compare different approaches

**Implementation:**
- [ ] I can implement features independently
- [ ] I can debug issues effectively
- [ ] I can extend the code

**Analysis:**
- [ ] I can read CPython source comfortably
- [ ] I understand performance implications
- [ ] I can evaluate trade-offs

**Application:**
- [ ] I can apply concepts to other projects
- [ ] I can teach these concepts to others
- [ ] I can design similar systems

## 🎓 Advanced Topics (Optional)

After completing all six phases, explore:

### **1. Optimization Techniques**
- Inline caching
- Just-in-time compilation
- Peephole optimization
- Register-based VMs

### **2. Advanced Features**
- Generators and coroutines
- Exception handling
- Module system
- Metaclasses

### **3. Alternative Designs**
- Register-based VM (like Lua)
- Threaded code interpretation
- Template JIT (like PyPy)
- Ahead-of-time compilation

### **4. Related Projects**
- Build a JavaScript interpreter
- Implement a Lisp interpreter
- Create a typed variant (like TypeScript)
- Design your own language

## 📚 Additional Resources

### **Books**
- "Crafting Interpreters" by Robert Nystrom
- "Engineering a Compiler" by Cooper & Torczon
- "Programming Language Pragmatics" by Scott
- "CPython Internals" by Anthony Shaw

### **Online Resources**
- CPython Developer's Guide
- Python Enhancement Proposals (PEPs)
- Python's AST module documentation
- Python's dis module documentation

### **Papers**
- See `docs/references/papers.md` for curated list

## 🤔 Common Questions

**Q: Should I implement everything from scratch?**
A: Yes, for learning! But study CPython's approach first.

**Q: How long does this take?**
A: 6-8 weeks for basics, 3-6 months for mastery.

**Q: What if I get stuck?**
A: 1) Read the ADR, 2) Study CPython, 3) Check checkpoint hints, 4) Discuss with others.

**Q: Can I skip phases?**
A: Not recommended. Each builds on previous understanding.

**Q: Should I optimize early?**
A: No! Get it working first, then optimize.

**Q: Is C knowledge required?**
A: Basic C helps, but you'll learn advanced C through this project.

## 🎯 Final Advice

1. **Be patient** - Understanding compilers takes time
2. **Read actively** - Don't just skim CPython code
3. **Test thoroughly** - Bugs hide in edge cases
4. **Reflect often** - Write down what you learn
5. **Enjoy the journey** - Building a language is magical!

---

**Ready to start?** Go to `HISTORICAL_TIMELINE.md` for the detailed roadmap, then begin with Phase 1!

**Need help?** Check the checkpoints for FAQs and hints.

**Happy Learning! 🎓**
