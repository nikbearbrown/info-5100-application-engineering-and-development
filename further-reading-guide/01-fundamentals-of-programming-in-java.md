# Module 1 — Fundamentals of Programming in Java: Further Reading

This chapter builds the conceptual foundation — reading code as a business model, distinguishing three kinds of wrong, and understanding why state and behavior belong together — but it deliberately does not teach Java syntax. To write and trace the lab programs that the assessments require, you need a reference that covers variables, data types, control flow, and basic I/O. These resources close that gap and extend the chapter's reasoning framework into two directions: practical Java mechanics for the exercises, and the empirical evidence behind the chapter's claims about novice errors and AI-assisted coding risks.

Read the Key resource before attempting Lab 1 or the three-integers exercise — it covers exactly the syntax the assessment requires. Choose one Recommended resource based on where you felt least certain: pick the first if the OOP model was unclear, the second if you want the "why" behind the design principles. The Further item is for students who want to understand the research claims the chapter makes about novice errors and AI tools; it is not required, and most students should skip it until after Module 3.

---

### Key

**The Java Tutorials: Learning the Java Language** — Oracle, continuously updated (Java SE 21)

I included this because the chapter teaches you how to read Java as a business model but does not teach you how to write it — and the lab assessments require writing. The Oracle Java Tutorials cover exactly the syntax this module's exercises depend on: primitive data types and variables ("Language Basics" section), `if-else` and loop control flow ("Control Flow Statements"), `String` operations, and `System.out` I/O. Read the "Language Basics" and "Control Flow Statements" sections before attempting the Lab 1 or the three-integers exercise; each subsection is short (5–10 minutes) and maps directly to one exercise type. When you encounter a construct in the lab starter code that you cannot name, use the tutorial's table of contents as an index rather than reading linearly. Available free at [https://docs.oracle.com/javase/tutorial/java/index.html](https://docs.oracle.com/javase/tutorial/java/index.html).

---

### Recommended

**Effective Java, Third Edition** — Joshua Bloch, 2018 (Addison-Wesley)

This book is the industry-standard reference for Java design reasoning, and Chapter 2 ("Creating and Destroying Objects") and Item 15 ("Minimize the accessibility of classes and members") speak directly to the encapsulation argument the chapter makes — that state and behavior belong together and that the only legitimate door into an object's state is the object's own behavior. Read Items 15–17 (pages 95–112), which cover encapsulation and immutability in concrete terms. The chapter asks you to argue why a three-book limit should live inside `Patron` rather than `Library`; Bloch gives you the vocabulary and reasoning to make that argument precisely. This is worth reading before Exercise 8 in the module. Institutional library access or O'Reilly Learning subscription is typical; the third edition is also widely available in university libraries.

**Head First Java, 3rd Edition** — Kathy Sierra, Bert Bates, and Trisha Gee, 2022 (O'Reilly)

I included this because some students encounter the object model as an abstract claim first and a concrete pattern second — this book reverses that order deliberately. Chapters 2–4 ("A Trip to Objectville," "Know Your Variables," "How Objects Behave") use visual, worked examples to build the same state-and-behavior intuition this module introduces through the library domain, but with multiple domains side by side so the pattern becomes recognizable rather than domain-specific. Read Chapter 2 (approximately 30 pages) after finishing this module's chapter if the object model still feels like a definition you memorized rather than a design principle you understand. The 3rd edition (2022) covers Java 17 and is available through O'Reilly Learning and most university libraries.

---

### Further

**"Learning and Teaching Programming: A Review and Discussion"** — Anthony Robins, Janet Rountree, and Nathan Rountree, *Computer Science Education*, 13(2), 2003, pages 137–172

This is a specialist literature review, not an introductory resource. It assumes comfort with basic programming concepts and academic reading conventions; plan for 60–90 minutes and a second read of the sections you mark. The prerequisite is that you have already completed at least one programming exercise and noticed a gap between what you expected the code to do and what it actually did — the payoff is understanding why that gap is systematic and not a personal failure. The chapter cites this paper to support claims about why novice programmers find silent wrong behavior harder to detect than compilation errors; Robins et al. survey the empirical evidence behind that claim across decades of CS education research, covering mental models, tracing skills, and the specific error categories that novices consistently misread. What the Recommended tier cannot give you is the evidence base: this paper is where the chapter's pedagogical choices come from, and reading it will let you evaluate those choices rather than simply accept them. Available through most university library databases (e.g., Taylor & Francis Online) via institutional access; DOI: 10.1076/csed.13.2.137.14200.

---

> **Assessment connection:** The Key resource (Oracle Java Tutorials, "Language Basics" and "Control Flow Statements" sections) directly supports Lab 1 — Fundamentals of Programming and the Optional Exercise: Java Program with Three Integers, both of which require writing variables, data types, and control flow constructs that the chapter text introduces conceptually but does not demonstrate syntactically.
