## Further Reading — Module 1: Fundamentals of Programming in Java

> **Content note:** Despite the title "Fundamentals of Programming in Java," this chapter does not cover Java syntax. Its actual subject is the object-oriented design principle — why state and behavior belong together, what distinguishes three kinds of wrong, and how to read running code as a business model. This guide addresses that actual content, plus the syntax gap the lab assessments expose.

The chapter leaves two gaps that matter in different ways. The first is practical: the lab assessments require writing variables, loops, and I/O constructs that the chapter never demonstrates — it teaches you to read and reason about Java, not to produce it. The second is conceptual: the chapter makes strong claims (about where behavior should live, about why novice errors are systematically hard to detect, about what OOP was designed to solve) without showing you the evidence or the intellectual history behind those claims. Whether those claims are right is not obvious, and understanding why they are right is what turns a rule into a design principle you can apply.

Read the Key resource before Lab 1 — it covers exactly the syntax the exercises require. Choose one Recommended resource based on where you felt least certain: the first if the object model still feels like a definition rather than a principle you can use, the second if you want the encapsulation argument in precise, professional terms before Exercise 8. The Further item is for students who want to evaluate the chapter's pedagogical claims rather than simply accept them; it is not required for any assessment, and most students should skip it until after Module 3.

---

### Key

**The Java Tutorials: Learning the Java Language — "Language Basics" and "Control Flow Statements"** — Oracle, continuously updated (Java SE 21) | https://docs.oracle.com/javase/tutorial/java/index.html

I included this because the chapter teaches you to read Java as a business model but does not teach you to write it — and the lab assessments require writing. The Oracle Java Tutorials are the authoritative, version-consistent reference for the syntax this module's exercises depend on: primitive types and variable declarations ("Language Basics"), `if-else` and `for`/`while` loop structures ("Control Flow Statements"), `String` handling, and `System.out` I/O. Read the "Language Basics" and "Control Flow Statements" sections before attempting Lab 1 or the three-integers exercise; each subsection runs 5–10 minutes and maps directly to one exercise type. When you encounter a construct in the starter code you cannot name, use the tutorial's sidebar as an index rather than reading linearly — you are using it as a reference, not a narrative. Available free; no institutional access required.

> Supports: Optional Lab — Fundamentals of Programming and Optional Exercise: Java Program with Three Integers, both of which require writing variables, data types, and control flow constructs the chapter introduces conceptually but never demonstrates syntactically.

---

### Recommended

**Head First Java, 3rd Edition** — Kathy Sierra, Bert Bates, and Trisha Gee, 2022 (O'Reilly) | ISBN: 978-1-491-91007-9

I included this because some students encounter the object model as an abstract definition first and a recognizable pattern second — this book deliberately reverses that order. Chapters 2 through 4 ("A Trip to Objectville," "Know Your Variables," "How Objects Behave") build the state-and-behavior intuition this module introduces through the library domain, but with multiple domains side by side so the pattern becomes transferable rather than tied to one example. If, after finishing this module's chapter, the object model still feels like something you memorized rather than something you understand, read Chapter 2 (approximately 30 pages) — it will make the library's `Patron` and `Book` design feel obvious rather than arbitrary. The 3rd edition covers Java 17, which is close enough to Java 21 that nothing in Chapters 2–4 diverges from this course. Available via O'Reilly Learning and most university libraries.

**Effective Java, Third Edition** — Joshua Bloch, 2018 (Addison-Wesley) | ISBN: 978-0-13-468599-1

This is the industry-standard reference for Java design reasoning, and I included it specifically for Exercise 8, which asks you to argue whether the three-book limit belongs inside `Patron` or inside `Library`. The chapter gives you the intuition; Bloch gives you the vocabulary and the evidence. Items 15 through 17 — "Minimize the accessibility of classes and members," "In public classes, use accessor methods, not public fields," and "Minimize mutability" — translate the chapter's claim that "state and behavior belong together" into precise, enforceable design rules. Read these three items (the "Minimizing Accessibility" and "Minimizing Mutability" sections of Chapter 4) before writing your Exercise 8 argument. This book is not a tutorial; skim the code examples and focus on Bloch's reasoning in the surrounding prose. Available via O'Reilly Learning and widely held in university libraries.

---

### Further

**"Learning and Teaching Programming: A Review and Discussion"** — Anthony Robins, Janet Rountree, and Nathan Rountree, *Computer Science Education*, 13(2), 2003, pages 137–172 | DOI: 10.1076/csed.13.2.137.14200

This is a specialist literature review written for CS education researchers — it is not a student text, and it assumes academic reading fluency and comfort with research methodology; budget 60–90 minutes and expect to read the key sections twice. The prerequisite is that you have already completed at least one programming exercise and noticed a gap between what you predicted the code would do and what it actually did: without that felt experience, the paper's findings will seem abstract. The payoff — what neither the chapter nor the Recommended resources provide — is the evidence base. The chapter asserts that silent wrong behavior is systematically harder for novice programmers to detect than compilation errors; Robins et al. survey the empirical research behind that claim across decades of CS education studies, covering how novices build (and misapply) mental models, why tracing errors are disproportionately persistent, and which error categories consistently resist self-correction. Reading this turns the chapter's pedagogical design from a set of rules into a position you can evaluate. Available through university library databases including Taylor & Francis Online via institutional access.

---

> **Assessment connection:** The Key resource (Oracle Java Tutorials, "Language Basics" and "Control Flow Statements" sections) directly supports Lab 1 — Fundamentals of Programming and the Optional Exercise: Java Program with Three Integers, both of which require writing variables, data types, and control flow constructs that the chapter introduces conceptually but does not demonstrate syntactically.
