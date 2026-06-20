## Further Reading — Module 9: Event-Driven Programming

> **Content note:** Despite the title "Module 9: Event-Driven Programming," this chapter covers Java Collections (`List`, `Map`, `Set`), the `Comparator` and `Comparable` interfaces, and the Stream API filter pipeline. The assessments reference JavaFX event-handler exercises, but the chapter body teaches collection-type selection, named ordering rules, and stream operations. This guide addresses the actual chapter content.

The chapter settles one question — which Java collection type matches which access pattern — but leaves a second one open: *how much does the choice matter, and when does "it compiles and runs" become "it fails in production"?* That tension between working code and correct code is not academic. Every Java developer has inherited a codebase that used `ArrayList` everywhere and then watched it slow to a crawl under real data. The deeper question — whether `Comparator` chaining and stream pipelines are best read as Java syntax or as an expression of a more general idea about separating data from behavior — is one the field has not fully resolved, and understanding it will help you read unfamiliar codebases faster. Read the Key resource before the lab submission. Choose one Recommended resource based on where the chapter felt shakiest: the `Comparator`/`Comparable` entry if the design-decision table was unclear, or the streams entry if the pipeline syntax felt mechanical rather than understood. The Further item is for students who want the theoretical underpinning — it is genuinely challenging and not required for the project.

---

### Key

**Java SE 21 API Documentation: Interface java.util.Comparator\<T\>** — Oracle, 2023 | https://docs.oracle.com/en/java/docs/jdk/21/api/java.base/java/util/Comparator.html

I included this because the chapter introduces `Comparator.comparing()`, `.thenComparing()`, `.reversed()`, and `Comparator.nullsFirst()`/`Comparator.nullsLast()` — four distinct methods — without showing their full signatures or explaining the type constraints that govern when chaining works. The API page gives the complete method list with signatures, the contract for `compare()` return values (negative/zero/positive), and explicit notes on null behavior. It also documents `Comparator.naturalOrder()` and `Comparator.reverseOrder()`, which are the building blocks the chapter uses without naming. Read the class-level description first (approximately five minutes), then locate the `comparing()`, `thenComparing()`, and `nullsFirst()` entries specifically — those three directly correspond to Exercises 2 and 3. When an AI-generated comparator throws a `NullPointerException`, this page is where you diagnose why and find the correct fix. Stable URL; version-consistent with Java 21.

> Supports: Lab exercise requiring three sort orders (Comparable natural order + two named Comparator objects), and Exercise 3 (null-handling in comparators using `nullsFirst`/`nullsLast`).

---

### Recommended

**"Lambda Expressions and Functional Interfaces" and "Working with Streams" in *Modern Java in Action*** — Raoul-Gabriel Urma, Mario Fusco, Alan Mycroft, 2019 | ISBN 978-1617293566

I included this because the chapter uses method references (`Book::getTitle`, `Book::isAvailable`) and lambda predicates inside `.filter()` without explaining what they are or why they work where they do. Students who follow the syntax without that explanation can copy examples but cannot adapt them when the predicate needs two conditions or the method reference needs a different signature. *Modern Java in Action* (Manning, 2nd edition) devotes Chapters 3 and 4 to lambda expressions and method references, then Chapters 5 and 6 to streams and collectors. Read Chapter 3 ("Lambda expressions") and the first half of Chapter 5 ("Working with streams"), which covers `filter`, `sorted`, and `collect`. Skip Chapter 6 (collectors beyond `toList`) unless Exercise 6's domain-transfer task prompts you to group elements — `Collectors.groupingBy` appears there. Available via institutional library; also available as a MEAP preview at manning.com.

**Item 14: "Consider implementing Comparable" in *Effective Java*, 3rd edition** — Joshua Bloch, 2018 | ISBN 978-0134685991

I included this because the chapter presents `Comparable` vs. `Comparator` as a design decision — use `Comparable` for the natural order, `Comparator` for everything else — without explaining *what makes an ordering "natural"* or what goes wrong when you implement `compareTo` incorrectly. Bloch's Item 14 is the canonical treatment: it defines the four contracts `compareTo` must satisfy (reflexivity, symmetry, transitivity, consistency with `equals`), explains why violating them produces subtle bugs rather than immediate failures, and shows when a `Comparator`-based approach is safer than `Comparable`. Read Item 14 in full (approximately 20 minutes). Pay particular attention to the discussion of floating-point comparisons and the warning about using subtraction as a shortcut — both are traps the chapter's exercises touch. Available via institutional library; also available at the O'Reilly Learning Platform with institutional access.

**Java SE 21 API Documentation: Interface java.util.Collection and java.util.Map** — Oracle, 2023 | https://docs.oracle.com/en/java/docs/jdk/21/api/java.base/java/util/Collection.html and https://docs.oracle.com/en/java/docs/jdk/21/api/java.base/java/util/Map.html

I included this because the chapter's collection-type selection table — `List` for ordered iteration, `Map` for keyed lookup, `Set` for membership testing — describes the *contracts* those interfaces make, but students who only read the chapter see the conclusion without seeing the interface itself. The `Collection` API page shows the operations every collection must support and which it may optionally support (e.g., `add` may throw `UnsupportedOperationException`). The `Map` page is particularly important for Exercise 7: the distinction between `HashMap` (no iteration order), `LinkedHashMap` (insertion order), and `TreeMap` (sorted order) is documented here and directly determines which `Map` implementation to recommend in the List-vs-Map parallel-index exercise. Read the class-level descriptions of both pages (approximately 15 minutes total); the method-level detail is reference material. Stable URLs; version-consistent with Java 21.

---

### Further

**Volume 3: *Sorting and Searching* in *The Art of Computer Programming*** — Donald E. Knuth, 1998 (3rd edition) | ISBN 978-0201896855

This is specialist literature written for algorithm researchers and advanced practitioners, not a student text — the mathematical notation is dense and the treatment assumes graduate-level comfort with discrete mathematics and combinatorics. The prerequisite for getting value from it is a solid understanding of O-notation as used in the chapter: you must be able to explain, without looking it up, why a `HashMap` lookup is O(1) average-case but O(n) worst-case, and what that distinction means in practice. If that reasoning still feels borrowed rather than owned, the Recommended resources will serve you better first. What this volume gives that the Recommended tier cannot is the *proof* behind the complexity claims the chapter states as facts: why comparison-based sorting cannot do better than O(n log n) in the general case (Section 5.3.1), what the constant factors are that O-notation hides, and how the choice between `Arrays.sort` and `Collections.sort` in Java maps onto different algorithmic strategies internally. After reading Sections 5.1 and 5.3.1 (approximately two to three hours, not a skim), the complexity column in the chapter's collection-selection table changes from a memorized rule into something you can derive. Available via institutional library.

---
