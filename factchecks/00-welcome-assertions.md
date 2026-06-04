# Assertions Report: 00-welcome.md
**Date:** 2026-05-25
**Source file:** chapters/00-welcome.md
**Assertions flagged:** 6
**Breakdown:** STAT: 0 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 0 | SPECIALIST: 5 | CURRENT: 1

---

## ⚠️ Critical — Requires Immediate Expert Review
None found.

---

## Full Findings

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** When you write Java, you write in a language humans can read. The computer cannot run that language directly. Before your program can execute, it has to be translated — *compiled* — into something the machine understands.
**Claim checked:** Java source must be compiled before this course's Java programs execute.
**Site visited:** https://docs.oracle.com/en/java/javase/21/docs/specs/man/javac.html
**Finding:** Oracle describes javac as the command that reads Java source files and compiles them into class files that run on the Java Virtual Machine.
**Expert review needed:** No
**Suggested reference:** Oracle. The javac Command. Java SE 21 / JDK 21 Tool Guides, 2023. https://docs.oracle.com/en/java/javase/21/docs/specs/man/javac.html
**Notes:** None.

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** The result of compilation is a `.class` file containing bytecode: a representation that is not quite machine code, but is much closer to it than the source you wrote.
**Claim checked:** javac compiles Java source into class files.
**Site visited:** https://docs.oracle.com/en/java/javase/21/docs/specs/man/javac.html
**Finding:** Oracle describes javac as the command that reads Java source files and compiles them into class files that run on the Java Virtual Machine.
**Expert review needed:** No
**Suggested reference:** Oracle. The javac Command. Java SE 21 / JDK 21 Tool Guides, 2023. https://docs.oracle.com/en/java/javase/21/docs/specs/man/javac.html
**Notes:** None.

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** That bytecode does not run directly on the hardware either. It runs inside a piece of software called the Java Virtual Machine, which reads the bytecode and executes it.
**Claim checked:** Java bytecode runs on a Java Virtual Machine.
**Site visited:** https://docs.oracle.com/javase/specs/jvms/se21/html/jvms-2.html
**Finding:** The JVM specification describes the runtime data areas and execution model used by Java Virtual Machine implementations.
**Expert review needed:** No
**Suggested reference:** Oracle. The Structure of the Java Virtual Machine. Java Virtual Machine Specification, Java SE 21, 2023. https://docs.oracle.com/javase/specs/jvms/se21/html/jvms-2.html
**Notes:** None.

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** The tool that contains the compiler — `javac` — is part of a package called the **JDK**, the Java Development Kit.
**Claim checked:** The JDK includes javac for Java compilation.
**Site visited:** https://docs.oracle.com/en/java/javase/21/docs/specs/man/javac.html
**Finding:** Oracle describes javac as the command that reads Java source files and compiles them into class files that run on the Java Virtual Machine.
**Expert review needed:** No
**Suggested reference:** Oracle. The javac Command. Java SE 21 / JDK 21 Tool Guides, 2023. https://docs.oracle.com/en/java/javase/21/docs/specs/man/javac.html
**Notes:** None.

### SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** Every Java application has exactly one entry point. Know where yours is.
**Claim checked:** Java applications are launched through a selected main class or entry point.
**Site visited:** https://docs.oracle.com/en/java/javase/21/docs/specs/man/java.html
**Finding:** Oracle documents java as the launcher for Java applications and the command used to run compiled Java code on the runtime.
**Expert review needed:** No
**Suggested reference:** Oracle. The java Command. Java SE 21 / JDK 21 Tool Guides, 2023. https://docs.oracle.com/en/java/javase/21/docs/specs/man/java.html
**Notes:** The sentence is pedagogically accurate for this course's single-entry application model. Java launch modes have additional details in the launcher specification.

### CURRENT — UNVERIFIED
**Assertion type:** POSITIVE
**Sentence:** *Current tool instructions, version-specific setup steps, and AI platform behavior require pre-offering verification.* [verify]
**Claim checked:** The chapter's setup and AI-platform instructions are current for the offering.
**Site visited:** No authoritative source identified
**Finding:** This is an explicitly version-sensitive course note. No stable authoritative source was identified for the current course offering at the time of this pass.
**Expert review needed:** Yes
**Suggested reference:** Could not identify a specific source
**Notes:** This was already marked [verify] in the source and should be checked against the live course environment before offering.

---

## Unverified Assertions
| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| *Current tool instructions, version-specific setup steps, and AI platform behavior require pre-offering verification.* [verify] | CURRENT | POSITIVE | This was already marked [verify] in the source and should be checked against the live course environment before offering. |

---

## AI-Pass Flags
No internal contradictions or clearly incorrect definitions found during this pass.
