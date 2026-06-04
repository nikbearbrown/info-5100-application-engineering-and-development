# Assertions Report: 13-collections-and-iterators.md
**Date:** 2026-05-25
**Source file:** chapters/13-collections-and-iterators.md
**Assertions flagged:** 4
**Breakdown:** STAT: 0 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 0 | SPECIALIST: 4 | CURRENT: 0

---

## ⚠️ Critical — Requires Immediate Expert Review
None found.

---

## Full Findings

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** `ArrayList` is a resizable-array implementation of the `List` interface.
**Claim checked:** ArrayList is a resizable-array List implementation.
**Site visited:** https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/ArrayList.html
**Finding:** Oracle documents ArrayList as a resizable-array List implementation with indexed access, automatic capacity growth, and documented iteration behavior.
**Expert review needed:** No
**Suggested reference:** Oracle. Class ArrayList. Java SE 21 API Specification, 2023. https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/ArrayList.html
**Notes:** None.

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** `HashMap` stores key-value mappings and does not promise iteration order.
**Claim checked:** HashMap maps keys to values and does not guarantee order.
**Site visited:** https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/HashMap.html
**Finding:** Oracle documents HashMap as a Map implementation that stores key-value mappings and makes no ordering guarantees.
**Expert review needed:** No
**Suggested reference:** Oracle. Class HashMap. Java SE 21 API Specification, 2023. https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/HashMap.html
**Notes:** None.

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** An `Iterator` lets code traverse a collection without indexing into it directly.
**Claim checked:** Iterator traverses elements.
**Site visited:** https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/Iterator.html
**Finding:** Oracle documents Iterator as an interface for traversing elements and optionally removing elements during iteration.
**Expert review needed:** No
**Suggested reference:** Oracle. Interface Iterator. Java SE 21 API Specification, 2023. https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/Iterator.html
**Notes:** None.

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** A `Comparator` defines an ordering rule that can be passed to sorting code.
**Claim checked:** Comparator imposes order on objects.
**Site visited:** https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/Comparator.html
**Finding:** Oracle documents Comparator as a comparison function that imposes an ordering on objects.
**Expert review needed:** No
**Suggested reference:** Oracle. Interface Comparator. Java SE 21 API Specification, 2023. https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/Comparator.html
**Notes:** None.

---

## Unverified Assertions
None found.

---

## AI-Pass Flags
No internal contradictions or clearly incorrect definitions found during this pass.
