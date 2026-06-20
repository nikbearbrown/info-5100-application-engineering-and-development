# Module 2 — Methods, Arrays, and File Objects: Further Reading

This chapter builds the reference-vs-object mental model carefully, but the module's assessed work — writing methods, searching arrays, and reading and writing files — goes well beyond what the chapter text covers. These resources close those gaps: the Key resource prepares you for the array and file I/O exercises directly; the Recommended resources deepen your understanding of method design and the `equals()`/`==` distinction introduced in Exercise 7; the Further resource explains why Java made the design choices it did, which is the kind of understanding that makes debugging feel like reasoning rather than guessing.

Read the Key resource before attempting the "Searching an Array" and "Reading from a File" assessments. Choose one Recommended resource based on whichever concept felt least settled after the chapter — method return types, or the identity-vs-equality gap. The Further item is optional; it is listed for students who want to understand *why* Java works this way, not just *that* it does.

### Key

**The Java™ Tutorials: "Arrays" and "The switch Statement" — Learning the Java Language trail** — Oracle, continuously updated (Java SE 21 edition)
[https://docs.oracle.com/javase/tutorial/java/nutsandbolts/arrays.html](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/arrays.html)

I included this because the chapter covers objects and references but leaves arrays largely unaddressed, yet three of the module's seven assessments require array traversal and file I/O. The "Arrays" section of Oracle's official tutorial (one short page plus the immediately following "Summary of Variables" section) covers array declaration, initialization with `new`, index-based access, and `array.length` — exactly the mechanics needed for the "Searching an Array" exercise. Read the Arrays page and the "Reading from a File" tutorial section (under the "Basic I/O" trail at [https://docs.oracle.com/javase/tutorial/essential/io/scanning.html](https://docs.oracle.com/javase/tutorial/essential/io/scanning.html)) before the file I/O assessments; skim rather than memorize, and keep the page open while writing your first `Scanner`-based file reader. This is official documentation: it will not go out of date between semesters, and it is the reference your instructor will use when grading for correctness.

### Recommended

**Effective Java, 3rd Edition — Chapter 3: "Methods Common to All Objects"** — Joshua Bloch, 2018, Addison-Wesley
(Items 10–14, pages 49–90; available through most university library systems via O'Reilly Learning)

Exercise 7 asks you to implement `equals()` and explain why Java does not make `==` do content equality by default. Bloch's Item 10 ("Obey the general contract when overriding equals") is the definitive treatment of this question — it names the five properties a correct `equals()` must satisfy (reflexivity, symmetry, transitivity, consistency, non-nullity) and shows exactly how a naive implementation breaks each one. Read Items 10 and 11 (which covers `hashCode()`, the method that must be overridden alongside `equals()`) before submitting Exercise 7. You do not need the rest of Chapter 3 for this module. Bloch writes for practicing developers, not beginners, but Items 10–11 are self-contained enough that a student who has completed this module's chapter can follow them — go slowly on the contract properties and you will be fine.

**Head First Java, 3rd Edition — Chapter 4: "How Objects Behave: Object State Affects Method Behavior"** — Kathy Sierra and Bert Bates, 2022, O'Reilly Media
(Chapter 4, pages 95–130; also available in print and via O'Reilly Learning)

The chapter you just read explains *what* methods are and establishes the reference model; this chapter of Head First Java shows *how* methods and instance state interact — specifically, how a method can read and modify the fields of the object it belongs to, what return types mean in practice, and how parameter passing works when objects (references) are passed rather than primitives. I included it because the "Methods" and "getDouble() Methods" assessments require you to design methods with specific return types and input-validation logic, and students who skip this often treat methods as arbitrary syntax rather than as behaviors owned by specific objects. Read the chapter once through at conversational pace; the visual layout is intentional and the puzzles embedded in the chapter are worth doing rather than skipping.

### Further

**The Java Virtual Machine Specification, Java SE 21 Edition — Chapter 2: "The Structure of the Java Virtual Machine"** — Oracle, 2023
[https://docs.oracle.com/javase/specs/jvms/se21/html/jvms-2.html](https://docs.oracle.com/javase/specs/jvms/se21/html/jvms-2.html)

*Level note: This is a language specification written for compiler implementors and advanced language engineers. It is not a tutorial and does not adapt to novice readers.* Prerequisite: you should be fully comfortable with the stack/heap mental model from this chapter, have completed all seven exercises, and understand what a reference variable holds and why `==` tests addresses rather than content. The payoff that the Recommended tier cannot give you: this document explains precisely where the stack ends and the heap begins in the JVM's memory model (Section 2.5), what the method area is, and why garbage collection works the way it does — the questions Exercise 6 raises ("what happens when no reference points to an object?") are answered here with full technical precision. Read Sections 2.5.1 (the Java Virtual Machine Stacks), 2.5.3 (the Heap), and 2.6 (Frames) — roughly 8 pages total — and nothing else from this document on a first pass. Return to it when you feel the mental model you have is a simplification you want to replace with the real thing.

---

> **Assessment connection:** The Key resource's Arrays page and Basic I/O scanning tutorial directly support the "Searching an Array" and "Reading from a File" assessments. Before writing your first array-traversal loop or `Scanner`-based file reader, read those two Oracle tutorial pages and keep them open; the syntax for declaring an array, iterating with `array.length`, and opening a file with `Scanner` is all there and matches exactly what the assessments require.
