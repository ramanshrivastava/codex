# Mini-CPython Quick Start Guide

> **Get started building a Python interpreter in 10 minutes!**

## 🚀 Quick Start

### 1. Clone and Navigate
```bash
cd /home/user/codex/mini-cpython
```

### 2. Read the Roadmap (5 minutes)
```bash
# Understand what you'll build
cat README.md

# See the timeline
cat HISTORICAL_TIMELINE.md
```

### 3. Start Phase 1 (Tokenizer)
```bash
# Study the design
cat docs/adrs/001-tokenizer-design.md

# Study CPython's implementation
less /home/user/cpython/Parser/lexer/lexer.c

# Understand tokens
cat /home/user/cpython/Grammar/Tokens
```

### 4. Implement Your First Tokenizer
```bash
cd src/lexer
# Create tokenizer.h and tokenizer.c
# Follow Phase 1.1 from ADR-001
```

### 5. Test It
```bash
# Create tests
cd ../../tests/unit
# Write test_tokenizer.c

# Compile and run
make test-tokenizer
./test-tokenizer
```

## 📚 Learning Path

### Week 1: Tokenizer
- **Day 1-2:** Study ADR-001, implement basic tokens (numbers, operators)
- **Day 3-4:** Add strings and identifiers
- **Day 5-6:** Implement indentation handling (the hard part!)
- **Day 7:** Error handling and cleanup

**Outcome:** Working tokenizer that converts Python source → tokens

### Week 2: Parser
- **Day 1-2:** Study ADR-005, design AST nodes
- **Day 3-4:** Implement expression parser
- **Day 5-6:** Add statement parser
- **Day 7:** Control flow and functions

**Outcome:** Parser that converts tokens → AST

### Week 3: Compiler
- **Day 1-2:** Study ADR-010, implement symbol table
- **Day 3-4:** Design bytecode instruction set
- **Day 5-6:** Implement code generator
- **Day 7:** Assembly and optimization

**Outcome:** Compiler that converts AST → bytecode

### Week 4: Virtual Machine
- **Day 1-2:** Study ADR-014, implement stack machine
- **Day 3-4:** Add variable storage and scopes
- **Day 5-6:** Implement control flow
- **Day 7:** Function calls and returns

**Outcome:** VM that executes bytecode

### Week 5: Object System
- **Day 1-2:** Study ADR-018, design object model
- **Day 3-4:** Implement int and str types
- **Day 5-6:** Add list and dict
- **Day 7:** Integration and testing

**Outcome:** Type system with built-in types

### Week 6: Runtime
- **Day 1-2:** Study ADR-021, implement reference counting
- **Day 3-4:** Build REPL
- **Day 5-6:** Add error handling
- **Day 7:** Final integration and celebration! 🎉

**Outcome:** Complete mini Python interpreter!

## 🎯 Daily Routine

**Morning (1-2 hours):**
1. Read the ADR for current phase
2. Study related CPython code
3. Plan implementation approach

**Afternoon (2-3 hours):**
1. Implement features incrementally
2. Write tests as you go
3. Debug and refine

**Evening (30 minutes):**
1. Complete checkpoint quiz
2. Write reflection notes
3. Prepare for next day

## 📊 Progress Tracking

### Week 1 Checklist
- [ ] Token structure defined
- [ ] Basic tokenizer works for numbers
- [ ] Operators recognized
- [ ] Strings and identifiers work
- [ ] Keywords recognized
- [ ] Indentation handled correctly
- [ ] Error messages shown
- [ ] Unit tests pass
- [ ] Checkpoint 1 completed

### Week 2 Checklist
- [ ] AST nodes defined
- [ ] Expression parser works
- [ ] Statement parser works
- [ ] Control flow parsed
- [ ] Functions parsed
- [ ] AST printer works
- [ ] Integration tests pass
- [ ] Checkpoint 2 completed

### Week 3 Checklist
- [ ] Symbol table built
- [ ] Bytecode format defined
- [ ] Expression compilation works
- [ ] Statement compilation works
- [ ] Control flow compiled
- [ ] Disassembler works
- [ ] Integration tests pass
- [ ] Checkpoint 3 completed

### Week 4 Checklist
- [ ] Stack machine works
- [ ] Variables load/store
- [ ] Control flow executes
- [ ] Functions call/return
- [ ] Stack frames work
- [ ] Debugger works
- [ ] Integration tests pass
- [ ] Checkpoint 4 completed

### Week 5 Checklist
- [ ] Base object system works
- [ ] Int type works
- [ ] Str type works
- [ ] List type works
- [ ] Dict type works
- [ ] Type dispatch works
- [ ] Integration tests pass
- [ ] Checkpoint 5 completed

### Week 6 Checklist
- [ ] Reference counting works
- [ ] No memory leaks
- [ ] REPL works
- [ ] Error handling works
- [ ] Can run Python programs
- [ ] All tests pass
- [ ] Checkpoint 6 completed

## 🛠️ Tools You'll Need

### Required
- C compiler (GCC or Clang)
- Make
- Git
- Text editor (VSCode, Vim, Emacs, etc.)

### Optional but Helpful
- GDB (debugger)
- Valgrind (memory leak detector)
- Python 3 (to compare output)

## 💡 Tips for Success

### 1. Read Before Coding
Don't jump straight to implementation. Understanding WHY is more important than WHAT.

### 2. Start Small
Implement the minimal version first. You can always add features later.

### 3. Test Early and Often
Write tests as you implement features. Bugs are easier to find when code is small.

### 4. Compare with CPython
When stuck, read how CPython does it. But don't copy blindly - understand first.

### 5. Take Notes
Write down your "aha!" moments. They're valuable for learning.

### 6. Don't Optimize Prematurely
Get it working first. Make it fast later (if needed).

### 7. Ask Questions
Use the checkpoints and exercises. They're designed to deepen understanding.

## 🎓 Learning Resources

### Inside This Project
- `README.md` - Project overview
- `LEARNING_GUIDE.md` - Detailed learning instructions
- `HISTORICAL_TIMELINE.md` - Python's evolution
- `docs/adrs/` - Architecture decision records
- `docs/checkpoints/` - Self-assessment quizzes
- `docs/comparisons/` - Mini vs CPython comparisons

### CPython Source
- `/home/user/cpython/` - Full CPython source
- Focus on: Parser/, Python/, Objects/, Include/

### External Resources
- **CPython Internals (Anthony Shaw):** Book on CPython
- **Crafting Interpreters (Robert Nystrom):** Excellent compiler book
- **Python Dev Guide:** https://devguide.python.org/
- **PEPs:** https://peps.python.org/

## 🐛 When You Get Stuck

### 1. Read the ADR
The architecture decision record explains the WHY and design rationale.

### 2. Check the Checkpoint
Learning checkpoints have hints and common pitfalls.

### 3. Study CPython
Look at how the real implementation handles it.

### 4. Simplify
Can you make the problem smaller? Solve a subset first.

### 5. Debug Systematically
- Print current state
- Use GDB to step through
- Write a minimal test case

### 6. Take a Break
Sometimes stepping away helps. Your brain keeps working!

## 🎉 Celebrate Milestones!

### Milestone 1: First Token
When your tokenizer recognizes its first number - celebrate! 🎊

### Milestone 2: First Parse
When your parser builds its first AST - celebrate! 🎊

### Milestone 3: First Bytecode
When your compiler generates its first instruction - celebrate! 🎊

### Milestone 4: First Execution
When your VM executes `2 + 2` - celebrate! 🎊

### Milestone 5: First Function Call
When you can call a function - celebrate! 🎊

### Milestone 6: First Program
When you run a real Python program - CELEBRATE BIG! 🎉🎉🎉

## 📅 Suggested Schedule

### Full-Time (6-8 weeks)
- 4-6 hours per day
- Complete all 6 phases
- Do all exercises
- Achieve mastery

### Part-Time (3-6 months)
- 1-2 hours per day
- Focus on core features
- Skip some exercises
- Solid understanding

### Casual (6-12 months)
- Few hours per week
- Take your time
- Enjoy the journey
- Deep appreciation

## 🎯 Success Metrics

After completing this project, you should be able to:

✅ Explain how Python executes code from source to result
✅ Read and understand CPython source code
✅ Implement a new language feature
✅ Debug Python internals issues
✅ Contribute to Python discussions
✅ Design your own programming language
✅ Teach compiler concepts to others

## 🚀 Ready to Start?

```bash
# Read the learning guide
cat LEARNING_GUIDE.md

# Read the timeline
cat HISTORICAL_TIMELINE.md

# Start Phase 1!
cat docs/adrs/001-tokenizer-design.md

# Begin implementation
cd src/lexer
vim tokenizer.h tokenizer.c
```

**Good luck and enjoy the journey! 🎓🐍**

---

*Remember: The goal is not just to build an interpreter, but to deeply understand how programming languages work. Take your time, experiment, and have fun!*
