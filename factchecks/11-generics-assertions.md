# Assertions Report: 11-generics.md
**Date:** 2026-05-25
**Source file:** chapters/11-generics.md
**Assertions flagged:** 2
**Breakdown:** STAT: 0 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 0 | SPECIALIST: 2 | CURRENT: 0

---

## ⚠️ Critical — Requires Immediate Expert Review
None found.

---

## Full Findings

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** It works because `EventHandler<ActionEvent>` is a functional interface — it has exactly one abstract method. Java can infer what the lambda is implementing.
**Claim checked:** EventHandler is a functional interface suitable for lambda expressions.
**Site visited:** https://openjfx.io/javadoc/21/javafx.base/javafx/event/EventHandler.html
**Finding:** OpenJFX documents EventHandler as a functional interface for receiving and handling events.
**Expert review needed:** No
**Suggested reference:** OpenJFX. Interface EventHandler. JavaFX 21 API Specification, 2023. https://openjfx.io/javadoc/21/javafx.base/javafx/event/EventHandler.html
**Notes:** None.

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** A lambda expression is Java syntax for supplying behavior where a functional interface is expected.
**Claim checked:** Lambda expressions target functional interfaces.
**Site visited:** https://docs.oracle.com/javase/specs/jls/se21/html/jls-15.html#jls-15.27
**Finding:** The Java Language Specification defines lambda expressions and their target typing against functional interfaces.
**Expert review needed:** No
**Suggested reference:** Oracle. Lambda Expressions. Java Language Specification, Java SE 21, 2023. https://docs.oracle.com/javase/specs/jls/se21/html/jls-15.html#jls-15.27
**Notes:** None.

---

## Unverified Assertions
None found.

---

## AI-Pass Flags
No internal contradictions or clearly incorrect definitions found during this pass.
