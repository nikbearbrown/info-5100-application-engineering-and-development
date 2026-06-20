# Module 8 — Abstract Classes and Interfaces: Further Reading

This chapter introduces file persistence as it works in a single-user, single-process context with plain CSV. What it does not cover are the failure modes that appear when field values contain commas, when the JVM is interrupted mid-write, or when you need to move from flat-file storage to a format that scales. These resources extend that foundation to robust I/O patterns, structured data formats, and the broader Java I/O class hierarchy — knowledge you will need before the persistence components of the semester project become nontrivial.

Read the Key resource before attempting Exercise 3 (writing explicit exception handlers) or Exercise 7 (the dirty-flag design challenge). Choose one Recommended resource based on which concept gave you the most trouble: pick the Oracle tutorial if the `java.io` class hierarchy felt opaque, or pick Bloch if you want to understand why `try-with-resources` is preferred over manual `close()` calls. The Further item is genuinely optional — skip it unless you are curious about how professional systems move beyond flat files.

---

### Key

**The Java Tutorials: Basic I/O** — Oracle, 2023
The Oracle Java Tutorials chapter on Basic I/O (available at docs.oracle.com/javase/tutorial/essential/io/) covers `BufferedReader`, `BufferedWriter`, `FileReader`, `FileWriter`, and the full `java.io` exception hierarchy — exactly the artifacts this chapter uses but does not fully explain. Focus on the "File I/O" and "Reading, Writing, and Creating Files" sections (approximately 15–20 minutes of reading). This resource directly supports the chapter's learning objective of understanding what `throws IOException` means and which specific subclasses map to which failure modes (file not found vs. permission denied vs. disk full). Before writing the exception handlers in Exercise 3, read the section on `IOException` and its subclasses so that your handlers catch the right exception at the right level rather than catching the root `Exception` class and swallowing everything. I included this because the chapter uses `BufferedReader` and `BufferedWriter` throughout without explaining the class hierarchy they belong to, and that gap will produce poorly scoped catch blocks without the background.

---

### Recommended

**Effective Java, 3rd Edition, Item 9: Prefer try-with-resources to try-finally** — Joshua Bloch, 2018
Bloch's Item 9 (pages 40–44) addresses exactly the resource-management pattern this chapter gets wrong in its initial code examples: manual calls to `reader.close()` and `writer.close()` in a finally block (or worse, without one). This resource deepens the chapter's treatment of exception handling by showing what happens when both the body of a try block and the close call throw exceptions simultaneously — a scenario the chapter does not discuss, but one that can silently suppress the original exception. Read this item before Exercise 4, which asks you to implement the update operation end-to-end; refactor your `saveToFile` and `loadFromFile` to use try-with-resources as you go. The item is four pages and takes roughly 10 minutes to read. I included this because the chapter's code samples use manual close, which is the pattern Bloch demonstrates as subtly dangerous, and students who copy that pattern into their projects will carry the defect forward.

**Oracle Java Tutorials: The try-with-resources Statement** — Oracle, 2023
Available at docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html, this short tutorial page (5–8 minutes) demonstrates the `try (BufferedReader br = new BufferedReader(...)) { }` syntax that replaces the manual close calls in this chapter's examples. It supports the chapter's exception-handling section by showing the Java language feature that makes the "what if the write fails partway through" policy question easier to implement correctly. Read this alongside or immediately after Exercise 3, and compare the try-with-resources version of `loadFromFile` to the version you wrote by hand — note specifically what happens to the `reader.close()` call in each version. This is a brief official reference, not a deep read; skim it once, then use it as a lookup reference when writing your persistence methods.

---

### Further

**Designing Data-Intensive Applications, Chapter 3: Storage and Retrieval** — Martin Kleppmann, 2017
This is a graduate-level and professional engineering text; it assumes comfort with data structures, file systems, and at least one semester of systems programming. The prerequisite for this chapter being rewarding is that you understand why the atomic-rename technique in Module 8 works (what "atomic" means at the OS level) — without that foundation, Kleppmann's treatment of log-structured storage and B-trees will be context-free. The payoff that the Recommended tier cannot provide: Kleppmann explains why flat-file persistence strategies like the ones in this chapter do not scale, what the professional alternatives are (append-only logs, LSM trees, B-tree indexes), and what trade-offs each one makes on the exact dimensions this chapter introduces — crash safety, write performance, and read performance. Chapter 3 (pages 69–99) takes approximately 90 minutes and will give you a durable mental model for why databases exist and what they replace. I included this because the chapter's "save-on-exit vs. save-after-every-mutation vs. atomic rename" table is a miniature version of the decision space Kleppmann maps at full scale, and students who want to understand that space professionally will find this the most direct path.

---

> **Assessment connection:** The Key resource (Oracle Basic I/O tutorial, "Reading, Writing, and Creating Files" section) directly supports Exercise 3, which asks you to write explicit exception handlers in `loadFromFile` for missing files, malformed lines, IO failures, and parse errors. Reading the `IOException` subclass hierarchy before writing those handlers will let you catch `FileNotFoundException` specifically for the missing-file case rather than catching the parent `IOException` for all cases and losing the ability to distinguish between "file never existed" and "disk error during read."
