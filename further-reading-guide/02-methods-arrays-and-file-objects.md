## Further Reading — Methods, Arrays, and File Objects

> **Content note:** Despite the title "Methods, Arrays, and File Objects," this chapter covers the reference-versus-object mental model: how Java allocates objects on the heap, how reference variables on the stack point to those objects, and what happens when two variables share a reference. Arrays and file objects appear only in the assessment table as separate exercises. This guide addresses the actual chapter content.

The chapter gives you the mental model but leaves two gaps that will surface the moment you move to method calls and domain-class design. The first gap is Java's parameter-passing convention: when you pass a `Patron` object to a method, does the method receive the object or the reference? The answer determines whether a method can mutate the original or only a local copy — and the chapter never addresses it. The second gap is `equals()`. The chapter notes that `==` tests reference equality, flags `equals()` as research territory in Exercise 7, and stops. But every domain class you write will eventually need content equality, and implementing it correctly requires understanding the contract inherited from `Object`.

Read the Key resource before Exercise 7 or any lab where you pass objects to methods. Choose one Recommended resource based on your stumbling point: the Oracle tutorial if parameter passing confused you during tracing, or Bloch's Item 10 if you want to implement `equals()` correctly before the next module. The Further resource is specialist territory — set it aside unless you want to understand why the informal model works, not just that it does. You are not expected to read all of this.

---

### Key

**"Passing Information to a Method or a Constructor"** — Oracle Java Tutorials, 2023 | https://docs.oracle.com/javase/tutorial/java/javaOO/arguments.html

I included this because the chapter builds the stack-and-heap model in detail but never applies it to method calls — the exact scenario where students first encounter unexpected mutations in their own code. This Oracle tutorial is the authoritative, version-consistent source for Java SE 21 that fills that gap directly. It explains Java's pass-by-value convention and shows explicitly that when you pass an object reference to a method, the method receives a copy of the reference, not a copy of the object — which means it can mutate the object through the reference but cannot redirect the caller's original variable. That distinction is invisible until you trace it, and the tutorial uses the same stack-and-heap framing the chapter establishes. Read the section titled "Passing Primitive Data Type Arguments" first to understand the baseline, then read "Passing Reference Data Type Arguments" and trace the examples against Exercise 5 from the chapter. Skim rather than memorize — the goal is to extend your trace practice to method boundaries before the next module introduces collections.

> Supports: Chapter Exercise 5 (shared-reference annotation exercise) and any lab that passes domain objects to helper methods

---

### Recommended

**"Overriding and Hiding Methods"** — Oracle Java Tutorials, 2023 | https://docs.oracle.com/javase/tutorial/java/IandI/override.html

I included this because the chapter introduces `toString()` as a method override without explaining what overriding means or what the `Object` contract requires. This tutorial explains the `@Override` annotation, the rules Java enforces when you override, and why `toString()` in `Object` is designed to be replaced rather than used as-is. That context makes `toString()` feel like a deliberate design decision rather than a magic incantation. The chapter's comparison of `display()` versus `toString()` — which ends with "toString() is the wider-reaching choice" — becomes fully interpretable once you understand the inheritance contract behind it. Read the section on instance method overriding and the subsection on `@Override`. Then return to your domain class from Exercise 3 and confirm your `toString()` override satisfies the contract. Treat this as a companion to Exercise 4; five to ten minutes of focused reading is sufficient.

**"Effective Java, Third Edition," Item 10: Obey the general contract when overriding equals** — Joshua Bloch, 2018 | ISBN 978-0-13-468599-1 (available via institutional library)

I included this because Exercise 7 asks students to implement `equals()` correctly and explain why Java does not make `==` do content equality — but the chapter provides no guidance on what "correct" actually requires. Bloch's Item 10 is the canonical treatment of the `equals()` contract in Java professional literature: it enumerates the five required properties (reflexive, symmetric, transitive, consistent, non-null) and shows precisely how each can be violated by code that looks plausible. The chapter's mental model of heap blocks and references is exactly the vocabulary Bloch assumes; you will find his framing reinforces rather than repeats what you have read. Read Item 10 only — the book is not meant to be read linearly, and the item is self-contained at roughly twelve pages. Use it as a checklist when implementing `equals()` for Exercise 7, verifying each of the five properties against your implementation before submission.

---

### Further

**"The Java Virtual Machine Specification, Java SE 21 Edition," Chapter 2: The Structure of the Java Virtual Machine** — Tim Lindholm, Frank Yellin, Gilad Bracha, Alex Buckley, and Daniel Smith, 2023 | https://docs.oracle.com/javase/specs/jvms/se21/html/jvms-2.html

This is the specification document that the chapter's informal stack-and-heap description approximates — it is written for JVM implementors and language engineers, not students, and reading it without preparation will feel like reading a legal contract in a second language. To get anything from it you need to be fully comfortable with the reference-versus-object model at the level of Exercise 5 and have at least a passing familiarity with what bytecode is; without that grounding, the precision becomes noise rather than clarity. If you have that preparation, Chapter 2 rewards close reading in two specific places: Section 2.5 ("Run-Time Data Areas") shows the formal partition of memory that the chapter's "stack" and "heap" are approximating, and Section 2.6 ("Frames") explains what is actually allocated when a method is called — which gives Exercise 6's open question ("what happens when no reference points to an object anymore?") a technically precise answer. What this gives that the Recommended tier does not is exactness: you will be able to say not just that references hold addresses but what the JVM guarantees about those addresses and what it deliberately leaves unspecified. Read Sections 2.5.1, 2.5.3, and 2.6 — roughly eight pages total — and nothing else from this document on a first pass.
