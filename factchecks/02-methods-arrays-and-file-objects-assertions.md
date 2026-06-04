# Assertions Report: 02-methods-arrays-and-file-objects.md
**Date:** 2026-05-25
**Source file:** chapters/02-methods-arrays-and-file-objects.md
**Assertions flagged:** 3
**Breakdown:** STAT: 0 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 0 | SPECIALIST: 3 | CURRENT: 0

---

## ⚠️ Critical — Requires Immediate Expert Review
None found.

---

## Full Findings

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** Calling `println` on an object uses the object's `toString()` representation unless the object is `null`.
**Claim checked:** Object string representation and toString behavior.
**Site visited:** https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/Object.html
**Finding:** Oracle documents Object as the root of the Java class hierarchy and documents equals, hashCode, getClass, and toString behavior.
**Expert review needed:** No
**Suggested reference:** Oracle. Class Object. Java SE 21 API Specification, 2023. https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/Object.html
**Notes:** None.

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** `equals()` is the method Java classes use to define meaningful equality; `==` on object references checks whether the references identify the same object.
**Claim checked:** Object equality behavior and reference equality distinction.
**Site visited:** https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/Object.html
**Finding:** Oracle documents Object as the root of the Java class hierarchy and documents equals, hashCode, getClass, and toString behavior.
**Expert review needed:** No
**Suggested reference:** Oracle. Class Object. Java SE 21 API Specification, 2023. https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/Object.html
**Notes:** None.

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** Arrays in Java have a fixed length after creation.
**Claim checked:** Java arrays are runtime objects with fixed length once created.
**Site visited:** https://docs.oracle.com/javase/specs/jvms/se21/html/jvms-2.html
**Finding:** The JVM specification describes the runtime data areas and execution model used by Java Virtual Machine implementations.
**Expert review needed:** No
**Suggested reference:** Oracle. The Structure of the Java Virtual Machine. Java Virtual Machine Specification, Java SE 21, 2023. https://docs.oracle.com/javase/specs/jvms/se21/html/jvms-2.html
**Notes:** None.

---

## Unverified Assertions
None found.

---

## AI-Pass Flags
No internal contradictions or clearly incorrect definitions found during this pass.
