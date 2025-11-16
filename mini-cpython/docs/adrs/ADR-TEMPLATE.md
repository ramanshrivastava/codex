# ADR-XXX: [Decision Title]

**Status:** [Proposed | Accepted | Deprecated | Superseded]
**Date:** YYYY-MM-DD
**Commit:** [git hash once implemented]
**Phase:** Phase X.Y
**CPython Reference:** `/home/user/cpython/[file]:[line-range]`
**Related PEPs:** [PEP numbers if applicable]
**Python Version:** Python X.Y (YYYY) - [Historical context]

---

## Context

### Problem Statement
[What problem are we solving? What are the requirements?]

### Constraints
- [Technical constraint 1]
- [Technical constraint 2]
- [Learning constraint - keep it simple for education]

### Current Situation
[What exists now? What led us to this decision point?]

---

## Decision

### What We Chose
[Clear, concise description of the approach we're taking]

### Implementation Overview
```c
// High-level code structure showing the approach
typedef struct {
    // ...
} DataStructure;

// Key function signatures
ReturnType key_function(Parameters);
```

---

## Rationale

### Why This Approach?

#### Reason 1: [Primary benefit]
[Detailed explanation]

#### Reason 2: [Secondary benefit]
[Detailed explanation]

#### Reason 3: [Learning value]
[Why this is good for understanding the concepts]

### Alternatives Considered

#### Alternative A: [Name]
**Description:** [How it would work]
**Pros:**
- [Advantage 1]
- [Advantage 2]

**Cons:**
- [Disadvantage 1]
- [Disadvantage 2]

**Why Rejected:** [Clear reason]

#### Alternative B: [Name]
[Same structure as Alternative A]

---

## CPython Comparison

### What CPython Does

**File:** `/home/user/cpython/[specific file]`
**Lines:** [specific line range]

**Approach:**
[Explanation of CPython's implementation]

**Key Differences from Our Approach:**
| Aspect | CPython | Mini-CPython | Why Different? |
|--------|---------|--------------|----------------|
| [Aspect 1] | [CPython approach] | [Our approach] | [Reason] |
| [Aspect 2] | [CPython approach] | [Our approach] | [Reason] |

**Code Comparison:**
```c
// CPython approach (simplified)
cpython_function() {
    // ...
}

// Our approach
our_function() {
    // Simpler version focusing on core concepts
    // ...
}
```

---

## Historical Evolution

### Python 0.9.0 (1991)
[How this was handled in the first Python]

### Python 1.X (1994-2000)
[Major changes or improvements]

### Python 2.X (2000-2010)
[Significant evolution]

### Python 3.X (2008-present)
[Modern approach]

### Key Milestones
- **Python X.Y (YYYY):** [What changed and why]
- **PEP XXX (YYYY):** [What it introduced]

---

## Trade-offs

### Benefits ✅
1. **[Benefit 1]:** [Explanation and impact]
2. **[Benefit 2]:** [Explanation and impact]
3. **[Benefit 3]:** [Explanation and impact]

### Limitations ❌
1. **[Limitation 1]:** [Explanation and impact]
   - *Mitigation:* [How we could address this]
2. **[Limitation 2]:** [Explanation and impact]
   - *Mitigation:* [How we could address this]

### Performance Implications
- **Time Complexity:** [Big-O analysis]
- **Space Complexity:** [Big-O analysis]
- **Compared to CPython:** [Faster/slower/same and why]

---

## Learning Outcomes

After implementing this, you should understand:

1. **[Concept 1]:** [What you'll learn]
   - Example: How lexical analysis separates concerns

2. **[Concept 2]:** [What you'll learn]
   - Example: Why indentation-based syntax is non-trivial

3. **[Concept 3]:** [What you'll learn]
   - Example: Trade-offs between simplicity and features

4. **[Practical Skill]:** [What you can do]
   - Example: Implement a tokenizer for a new language

5. **[Design Insight]:** [Deeper understanding]
   - Example: Why Python made certain design choices

---

## References

### CPython Source
- **Primary:** `/home/user/cpython/[main file]`
- **Related:** `/home/user/cpython/[related file]`
- **Tests:** `/home/user/cpython/Lib/test/test_[component].py`

### PEPs (Python Enhancement Proposals)
- **[PEP XXX](https://peps.python.org/pep-XXXX/):** [Title and relevance]

### Academic Papers
- **[Author], [Year]:** "[Paper Title]"
  - Key insight: [What it contributes]

### Git History
- **Initial implementation:** `git log --follow [file]`
- **Key commits:** [Significant changes]

### Documentation
- **Python docs:** https://docs.python.org/3/[relevant section]
- **Dev guide:** https://devguide.python.org/[relevant section]

---

## Implementation Checklist

Before marking this ADR as "Accepted", ensure:

- [ ] Implementation compiles without warnings
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] Code is documented with comments
- [ ] Comparison doc updated (`docs/comparisons/[component]-comparison.md`)
- [ ] Learning checkpoint updated
- [ ] Examples demonstrate the feature

---

## Exercises

### Exercise 1: Extend the Feature
**Task:** [Specific extension to implement]
**Difficulty:** ⭐⭐☆☆☆
**Time:** [Estimated time]
**Learning Goal:** [What you'll learn]

**Hints:**
- [Hint 1]
- [Hint 2]

### Exercise 2: Debug the Code
**Task:** [Intentional bug to find and fix]
**Difficulty:** ⭐⭐⭐☆☆
**Description:** [What breaks]

### Exercise 3: Read CPython
**Task:** [Specific CPython code to study]
**Questions to answer:**
1. [Question about implementation]
2. [Question about design choice]
3. [Question about edge cases]

---

## Revision History

| Date | Change | Reason |
|------|--------|--------|
| YYYY-MM-DD | Initial version | [Why created] |
| YYYY-MM-DD | [Update description] | [Why updated] |

---

## Notes

[Any additional notes, open questions, or future considerations]

---

**Next ADR:** ADR-XXX ([Next topic])
**Previous ADR:** ADR-XXX ([Previous topic])
**Related ADRs:** ADR-XXX, ADR-YYY ([How they relate])
