# Module 6 — Basics of GUI Programming in Java: Further Reading

This chapter establishes the habit of separating domain participants from credentials, hashing passwords with SHA-256, and asking the threat-model question before writing any authentication code. What it deliberately does not close is the gap between that course-project foundation and the production-grade decisions that follow it: why SHA-256 alone is not enough, what bcrypt and Argon2 actually do differently, and how the object-separation principle you practiced here connects to a broader design vocabulary. These resources extend that foundation to those decisions and to the failure modes that appear when real systems deviate from the design this chapter introduces.

Read the Key resource before submitting the Lab: Account Directory and Login Manager — it directly informs the threat-model table you are required to produce. Choose one Recommended resource based on whichever concept felt least settled after the chapter: pick the OWASP item if you want to know what comes after SHA-256, or the Java `MessageDigest` documentation if you want to verify your hash implementation details. The Further item is for students who want to understand the underlying cryptographic reasoning — it assumes comfort with the chapter's hashing concepts and will take about 90 minutes.

### Key

**OWASP Password Storage Cheat Sheet** — OWASP Foundation, 2024

I included this because the chapter names bcrypt, scrypt, and Argon2 as what production systems use but does not explain what they do that SHA-256 does not. This resource fills exactly that gap. Read the "Background" and "Password Hashing Algorithms" sections (approximately the first third of the page, up through the algorithm comparison table) — those sections explain salting, work factors, and why a deliberately slow hash function changes the attacker's cost calculation in ways that matter for your threat-model table. The learning outcome this supports is direct: the chapter asks you to write a threat-model row for "what would make the hashed design stronger," and this resource gives you the specific answer. Available free at owasp.org/www-project-cheat-sheets.

### Recommended

**Java SE 17 API Documentation: `java.security.MessageDigest`** — Oracle, 2021

The chapter provides the `hash()` method pattern but does not explain what `getInstance("SHA-256")` is selecting from, why the charset matters, or what happens when `digest()` is called twice on the same instance. The `MessageDigest` class documentation at docs.oracle.com/en/java/docs/api/java.base/java/security/MessageDigest.html covers the provider architecture, the one-shot vs. update/digest distinction, and thread-safety constraints — all of which are relevant to Exercise 2's step-by-step trace. Read the class-level description and the `getInstance`, `digest`, and `reset` method entries. This directly supports the verification habit the chapter builds: after implementing the `hash()` method, you should be able to explain what each line does from the specification, not just from the example.

**"Threat Modeling: Designing for Security"** — Adam Shostack, 2014 (Wiley)

The chapter introduces the threat-model habit as a single table with three rows. Shostack's book is the field reference for that practice at scale, and Chapter 1 ("Dive In and Threat Model!") covers the same question — "what can an attacker do?" — using the STRIDE framework in about 25 pages accessible to anyone who has finished this module. I included this because students who want to go beyond the course project's simplified table will find that the professional practice looks exactly like what the chapter describes, just with more systematic enumeration of threat categories. Read Chapter 1 only for this module; return to Chapter 3 ("STRIDE per Element") when you reach the authorization module. Available through most university library systems (O'Reilly Safari access or physical copy).

### Further

**"Password Security: A Case History"** — Robert Morris and Ken Thompson, *Communications of the ACM*, 1979 (Vol. 22, No. 11, pp. 594–597)

This is a primary source from the researchers who designed the original Unix password hashing scheme — the direct ancestor of the design pattern this chapter teaches. It is 46 years old, four pages long, and still the clearest explanation of why one-way hashing of passwords is the correct design move and what the attacker's problem actually is when they face a hashed store. The level note: this is a research paper written for a systems-programming audience; it assumes comfort with the concepts of one-way functions and dictionary attacks that the chapter introduces. The prerequisite is that you are confident in what the chapter covers — specifically, the distinction between what an attacker gains from plaintext storage versus hashed storage. The payoff is something the Recommended tier cannot give you: a concrete historical account of the original threat model reasoning, written by people who were designing against real attackers, which makes the design decisions in this chapter feel necessary rather than arbitrary. Read it as a 20-minute companion to your threat-model table, and notice which of your table's rows the 1979 threat model already anticipated. Available through ACM Digital Library (institutional access) or as a widely cached PDF.

---

> **Assessment connection:** The Key resource (OWASP Password Storage Cheat Sheet, "Password Hashing Algorithms" section) directly supports the Lab pre-submission requirement: before writing any code, you must produce a threat-model table with a row for "what would make the hashed design stronger." The OWASP item provides the specific technical answer — salting and adaptive work factors — that distinguishes a complete threat-model row from a vague one.
