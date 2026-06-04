# Assertions Report: 10-event-driven-programming-with-scene-builder.md
**Date:** 2026-05-25
**Source file:** chapters/10-event-driven-programming-with-scene-builder.md
**Assertions flagged:** 2
**Breakdown:** STAT: 0 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 0 | SPECIALIST: 2 | CURRENT: 0

---

## ⚠️ Critical — Requires Immediate Expert Review
None found.

---

## Full Findings

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** `FXMLLoader` reads an FXML file and constructs the corresponding object hierarchy.
**Claim checked:** FXMLLoader loads FXML object hierarchies.
**Site visited:** https://openjfx.io/javadoc/21/javafx.fxml/javafx/fxml/FXMLLoader.html
**Finding:** OpenJFX documents FXMLLoader as the loader for FXML object hierarchies and documents FXML annotation support for controller fields and methods.
**Expert review needed:** No
**Suggested reference:** OpenJFX. Class FXMLLoader and Annotation FXML. JavaFX 21 API Specification, 2023. https://openjfx.io/javadoc/21/javafx.fxml/javafx/fxml/FXMLLoader.html
**Notes:** None.

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** `@FXML` marks controller fields and methods that are connected to FXML-defined interface elements.
**Claim checked:** FXML annotation supports controller injection and method access.
**Site visited:** https://openjfx.io/javadoc/21/javafx.fxml/javafx/fxml/FXMLLoader.html
**Finding:** OpenJFX documents FXMLLoader as the loader for FXML object hierarchies and documents FXML annotation support for controller fields and methods.
**Expert review needed:** No
**Suggested reference:** OpenJFX. Class FXMLLoader and Annotation FXML. JavaFX 21 API Specification, 2023. https://openjfx.io/javadoc/21/javafx.fxml/javafx/fxml/FXMLLoader.html
**Notes:** None.

---

## Unverified Assertions
None found.

---

## AI-Pass Flags
No internal contradictions or clearly incorrect definitions found during this pass.
