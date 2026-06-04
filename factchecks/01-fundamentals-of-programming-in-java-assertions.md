# Assertions Report: 01-fundamentals-of-programming-in-java.md
**Date:** 2026-05-25
**Source file:** chapters/01-fundamentals-of-programming-in-java.md
**Assertions flagged:** 2
**Breakdown:** STAT: 0 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 0 | SPECIALIST: 2 | CURRENT: 0

---

## ⚠️ Critical — Requires Immediate Expert Review
None found.

---

## Full Findings

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** A compile error means Java could not translate the source file into bytecode.
**Claim checked:** Compilation errors occur before class-file generation succeeds.
**Site visited:** https://docs.oracle.com/en/java/javase/21/docs/specs/man/javac.html
**Finding:** Oracle describes javac as the command that reads Java source files and compiles them into class files that run on the Java Virtual Machine.
**Expert review needed:** No
**Suggested reference:** Oracle. The javac Command. Java SE 21 / JDK 21 Tool Guides, 2023. https://docs.oracle.com/en/java/javase/21/docs/specs/man/javac.html
**Notes:** None.

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** A runtime error means the program compiled, started executing, and then failed while it was running.
**Claim checked:** Runtime errors happen during execution, after launch.
**Site visited:** https://docs.oracle.com/en/java/javase/21/docs/specs/man/java.html
**Finding:** Oracle documents java as the launcher for Java applications and the command used to run compiled Java code on the runtime.
**Expert review needed:** No
**Suggested reference:** Oracle. The java Command. Java SE 21 / JDK 21 Tool Guides, 2023. https://docs.oracle.com/en/java/javase/21/docs/specs/man/java.html
**Notes:** None.

---

## Unverified Assertions
None found.

---

## AI-Pass Flags
No internal contradictions or clearly incorrect definitions found during this pass.
