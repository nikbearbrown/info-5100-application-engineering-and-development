# Assertions Report: 05-inheritance-and-polymorphism.md
**Date:** 2026-05-25
**Source file:** chapters/05-inheritance-and-polymorphism.md
**Assertions flagged:** 2
**Breakdown:** STAT: 0 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 0 | SPECIALIST: 2 | CURRENT: 0

---

## ⚠️ Critical — Requires Immediate Expert Review
None found.

---

## Full Findings

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** In Java, polymorphism means the method selected at runtime depends on the actual class of the object, not only on the declared type of the variable.
**Claim checked:** Java dynamic dispatch selects the implementation at runtime for instance methods.
**Site visited:** https://docs.oracle.com/javase/specs/jls/se21/html/jls-15.html#jls-15.12.4.4
**Finding:** The Java Language Specification describes runtime method selection for instance method invocation, confirming the dynamic dispatch behavior taught in the chapter.
**Expert review needed:** No
**Suggested reference:** Oracle. Method Invocation Expressions. Java Language Specification, Java SE 21, 2023. https://docs.oracle.com/javase/specs/jls/se21/html/jls-15.html#jls-15.12.4.4
**Notes:** None.

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** A subclass inherits accessible behavior and state structure from its superclass and may override methods.
**Claim checked:** Java inheritance and method overriding support runtime polymorphism.
**Site visited:** https://docs.oracle.com/javase/specs/jls/se21/html/jls-15.html#jls-15.12.4.4
**Finding:** The Java Language Specification describes runtime method selection for instance method invocation, confirming the dynamic dispatch behavior taught in the chapter.
**Expert review needed:** No
**Suggested reference:** Oracle. Method Invocation Expressions. Java Language Specification, Java SE 21, 2023. https://docs.oracle.com/javase/specs/jls/se21/html/jls-15.html#jls-15.12.4.4
**Notes:** None.

---

## Unverified Assertions
None found.

---

## AI-Pass Flags
No internal contradictions or clearly incorrect definitions found during this pass.
