# Module 8 — Abstract Classes and Interfaces: CRUD Lifecycle & CSV Persistence
## Exercise Set

**Learning Objectives**
1. Implement CSV-based `saveToFile()` and `loadFromFile()` operations
2. Design exception handling with explicit policy decisions
3. Choose and justify a save strategy based on data loss windows
4. Trace the object-to-file-to-object lifecycle through a complete example

---

## Tier 1 — Warm-Up

*(Tests: recall, vocabulary, true/false with explanation)*

---

**Exercise 1** (Tests: recall — CRUD operations)

What does CRUD stand for? Give one concrete example of each operation from a library catalog application. Each example should name the specific data being changed.

---

**Exercise 2** (Tests: true/false — in-memory persistence)

**True or False:** "Data stored in a Java `ArrayList` persists after the program closes, as long as the objects are still referenced."

State whether the claim is true or false, then write two to three sentences explaining what actually happens to in-memory data when a Java program exits.

---

**Exercise 3** (Tests: vocabulary — data loss window)

What is a **data loss window**? Give a specific example of when one occurs in an application that saves data only when the user closes it. How large is the data loss window in a typical student library project with no explicit save strategy?

---

**Exercise 4** (Tests: recall — CSV format)

What does CSV stand for, and why is it described as a "transparent format"? What makes it easier to debug than a binary or serialized object format?

---

**Exercise 5** (Tests: true/false — exception handling in student projects)

**True or False:** "Exception handling code can be omitted in student projects because `IOException`s are rare in practice."

State whether the claim is true or false, then write two to three sentences explaining what happens at runtime if `IOException` handling is omitted and the file is missing or unwritable.

---

## Tier 2 — Application

*(Tests: scenario design, error analysis, AI interaction)*

---

**Exercise 6** (Tests: CSV format design — hospital appointment system)

A hospital appointment system stores `Doctor` and `Appointment` objects. Design the CSV format for both.

**(a)** Write a sample CSV line for a `Doctor` object with fields: `id`, `name`, `specialty`, `phone`.

**(b)** Write a sample CSV line for an `Appointment` object with fields: `appointmentId`, `doctorId`, `patientId`, `date`, `time`.

**(c)** Explain why the `Appointment` CSV stores `doctorId` rather than the full doctor name and phone number. What problem would arise if the full doctor data were duplicated in each appointment line?

---

**Exercise 7 — Error Analysis** (Tests: error identification — saveToFile() method)

A student writes a `saveToFile()` method for a library catalog:

```java
public void saveToFile(String filename) {
    try {
        BufferedWriter writer = new BufferedWriter(new FileWriter(filename));
        for (Book book : catalog) {
            writer.write(book.toCSV());
        }
    } catch (IOException e) {
        System.out.println("Save failed.");
    }
}
```

Identify **two** problems in this method. For each problem:
- Name the problem
- Explain what goes wrong at runtime
- Write the corrected version of the relevant lines

---

**Exercise 8** (Tests: save strategy comparison — grade management system)

Compare three save strategies for a student grade management system. For each strategy:
- Describe the data loss window
- Name one scenario where it is the right choice
- Name one scenario where it fails unacceptably

The three strategies are:
- **(a)** Save on application exit
- **(b)** Save after every mutation (every time a grade is added or changed)
- **(c)** Save to a temporary file, then rename atomically (atomic rename)

---

**Exercise 9 — AI Interaction** (Tests: evaluating AI-generated persistence advice)

A student asks an AI assistant: *"How do I save my Java objects to a file?"*

The AI responds:

> "The easiest way is Java object serialization. Add `implements Serializable` to your class and use `ObjectOutputStream` to write objects directly. This is simpler than CSV because you don't need to parse anything."

Answer the following:

**(a)** Identify the strongest point in the AI's response (what, if anything, is correct or useful).

**(b)** Identify one significant limitation of Java object serialization that the AI did not mention. Consider what happens when you change a field name or add a field to the class after files have already been saved.

**(c)** Write a one-paragraph comparison of serialization vs CSV for a student project, covering at least: human readability, compatibility after class changes, and ease of debugging.

---

**Exercise 10** (Tests: exception policy design — loadFromFile() with malformed data)

A library catalog's `loadFromFile()` encounters a malformed CSV line — a line that has fewer fields than expected (for example, three fields where five are required).

Describe **three** different exception-handling policies the developer could choose, ranging from strictest to most lenient. For each policy:
- Describe the behavior when the malformed line is encountered
- Identify which real-world context would use this policy
- Name the risk of choosing it

---

## Tier 3 — Synthesis

*(Tests: cross-chapter integration — must name prior chapters explicitly)*

---

**Exercise 11** (Tests: Ch 8 + Ch 5 — persistence and supply-side startup sequence)

*This exercise connects Module 8 with Module 5.*

In Chapter 5, you built a supply-side catalog that preloads entities — such as `Book` and `Patron` objects — before any transactions are allowed to run. In Chapter 8, you learned that in-memory data does not persist across application restarts — it must be explicitly saved to and loaded from a file.

Combine both principles to describe the complete startup sequence for a library system that has both persistence and a supply-side model:

- In what order should `loadFromFile()` calls appear relative to catalog initialization and transaction availability?
- What does each `loadFromFile()` call populate, and what does "populated" mean in the context of the supply-side model from Chapter 5?
- What is the earliest point in startup at which a checkout transaction is safe to run, and what specific failure occurs if that point has not yet been reached?

A strong answer uses supply-side vocabulary from Chapter 5 (entities, preloading, independence) and names the specific runtime failure, not just a general warning about order.

---

**Exercise 12** (Tests: Ch 8 + Ch 4 — debugging persistence failures)

*This exercise connects Module 8 with Chapter 4.*

In Chapter 4, you learned to distinguish symptom from root cause when debugging. Apply this to a persistence bug: a hospital appointment system displays the correct appointments while it is running, but after the application is restarted, some appointments from the last session are missing.

**(a)** State a precise, falsifiable hypothesis about where state diverges between the running application and the reloaded state. Name the specific point where they separate.

**(b)** Identify the most likely root cause: is this a save strategy issue, a serialization error, or a partial-write failure? Explain your reasoning using one piece of evidence you would look for.

**(c)** Describe the breakpoint location and the specific variable you would inspect to confirm your hypothesis. What value would confirm the bug, and what value would rule it out?

A strong answer uses debugging vocabulary from Chapter 4 (symptom, proximate cause, root cause) and identifies a concrete inspection point, not just a general area of the code.

---

## Tier 4 — Challenge

*(No answer key. Rubric only.)*

---

**Exercise 13** (Tests: atomic rename limitations — logical vs physical data integrity)

The atomic rename save strategy — write to a temporary file, then rename to replace the original — is described as the safest common approach because the rename operation is atomic at the OS level: the original file is either fully replaced or not replaced at all.

Design a scenario where even atomic rename fails to protect data integrity: where the rename succeeds, the file is written completely, but the saved data is still wrong.

Your answer must address:

**(a)** The specific failure scenario (what went wrong in the application before `saveToFile()` was called)

**(b)** Why atomic rename did not help (what atomic rename does and does not guarantee)

**(c)** What additional mechanism would be needed to detect or prevent this failure

**(d)** The trade-off between implementation complexity and the data integrity guarantee the additional mechanism provides

**Rubric — a strong response will:**
- Identify a plausible logical corruption scenario (e.g., a mutation that was not applied correctly, a partial in-memory state, a concurrent modification) rather than a physical I/O failure
- Correctly explain what atomic rename guarantees (file is never half-written) and does not guarantee (application data is correct before write)
- Propose a concrete additional mechanism — not a vague suggestion like "validate the data" — such as a checksum, a transaction log, or an in-memory invariant check before save
- Make an explicit trade-off judgment: state what the mechanism costs (complexity, time, storage) and what it gains (detection of a specific failure class)

---

## Full Answer Key

*(Tiers 1–3 only)*

---

### Tier 1 Answers

**Exercise 1**
CRUD stands for Create, Read, Update, Delete.

Library catalog examples:
- **Create:** A librarian adds a new book record with ISBN `978-0-06-112008-4`, title *To Kill a Mockingbird*, and author *Harper Lee* to the catalog.
- **Read:** A patron searches for books by author and the system returns all matching `Book` objects from the catalog.
- **Update:** A librarian changes the available copy count for a book from 3 to 2 after a copy is damaged.
- **Delete:** A librarian removes a book record from the catalog because all copies have been lost or retired.

---

**Exercise 2**
**False.**

An `ArrayList` (and all Java objects) exists only in the JVM's heap memory. When the program exits, the operating system reclaims that memory. There is no automatic mechanism to persist in-memory data to disk — the data is gone the moment the JVM terminates. To survive a restart, data must be explicitly written to a file (or database) before the program exits.

---

**Exercise 3**
A data loss window is the period of time during which new or changed data exists only in memory and has not yet been written to the persistent file. If the application crashes, loses power, or is force-closed during this window, all changes made since the last successful save are permanently lost.

In an application that saves only on exit, the data loss window spans the entire session — from the first change after the last save to the moment the exit save completes. In a typical student library project with no explicit save strategy, a crash at any point during a session could lose all work done in that session, potentially hours of changes.

---

**Exercise 4**
CSV stands for Comma-Separated Values. It is called a "transparent format" because the data is stored as plain human-readable text — you can open the file in any text editor and immediately read the values without any special tool.

This makes it easier to debug than a binary format because you can visually inspect the file to verify that data was written correctly, check for missing fields, or spot encoding problems. A binary or serialized format is opaque — its contents appear as unreadable characters in a text editor, so you cannot confirm whether the write succeeded without running additional code.

---

**Exercise 5**
**False.**

`IOException`s are not rare — they occur whenever a file does not exist, a path is incorrect, the disk is full, or the program lacks permission to write to the specified location. These are all realistic conditions in a student project. If `IOException` handling is omitted, the code will not compile because Java's compiler enforces handling of checked exceptions. If a `try/catch` block is present but empty (or prints only a message), the program silently continues with no data saved or loaded, and the user receives no useful feedback about what went wrong.

---

### Tier 2 Answers

**Exercise 6**

**(a)** Sample Doctor CSV line:
```
D001,Dr. Maria Santos,Cardiology,617-555-0142
```

**(b)** Sample Appointment CSV line:
```
A1047,D001,P0293,2026-07-15,09:30
```

**(c)** The `Appointment` CSV stores `doctorId` rather than full doctor data because storing the full name and phone in every appointment line creates **data redundancy**. If Dr. Santos's phone number changes, you would have to update every appointment record she appears in — and if any are missed, the data becomes inconsistent. By storing only the ID, the appointment record is small and stable: it points to the `Doctor` record where the authoritative data lives. This is the same principle as the ID-based linking in Module 6: references by ID remain valid even when the referenced entity's details change.

---

**Exercise 7**

**Problem 1: The `BufferedWriter` is never closed**
The `writer.close()` call is missing. `BufferedWriter` buffers output in memory before flushing it to disk. If `close()` is never called, the buffer may never be flushed, and some or all data may not be written to the file. The file may appear to save but contain partial or empty content.

Corrected — use try-with-resources:
```java
try (BufferedWriter writer = new BufferedWriter(new FileWriter(filename))) {
    for (Book book : catalog) {
        writer.write(book.toCSV());
        writer.newLine();
    }
} catch (IOException e) {
    System.out.println("Save failed: " + e.getMessage());
}
```

**Problem 2: No newline written between records**
`writer.write(book.toCSV())` writes each CSV string without a line separator. All book records are written as one continuous string. When `loadFromFile()` reads the file line by line, it will read the entire file as a single line and produce one malformed record instead of many valid ones.

Corrected: add `writer.newLine()` after each `write()` call, as shown above.

---

**Exercise 8**

**(a) Save on application exit**
- Data loss window: the entire session from the first mutation to exit. If the application crashes, all session changes are lost.
- Right choice: a read-heavy system where changes are infrequent and each session's work is small (e.g., a personal note-taking app where sessions are short).
- Fails unacceptably: any long-running session or application that runs in an environment prone to crashes, power loss, or force-close (e.g., a hospital system recording appointments over a full workday).

**(b) Save after every mutation**
- Data loss window: the duration of a single write operation (milliseconds). Any change not yet written is at risk only for a very short window.
- Right choice: any system where losing even one record is unacceptable and write volume is low (e.g., a library checkout system recording loans).
- Fails unacceptably: a system with high mutation volume — saving after every keystroke in a text editor would cause perceptible lag and excessive disk writes.

**(c) Atomic rename (write to temp, then rename)**
- Data loss window: the same as save-on-mutation or save-on-exit, depending on when the save is triggered. The atomic rename addresses partial-write failure, not the frequency of saving.
- Right choice: any system where a partially written save file (from a crash mid-write) would corrupt existing data and make recovery impossible.
- Fails unacceptably: environments where the temp file and the target file are on different filesystems — a rename across filesystems is not atomic and may silently degrade to a copy-then-delete, losing the atomicity guarantee.

---

**Exercise 9**

**(a)** Strongest point: Java serialization does eliminate the need to write a parser. `ObjectOutputStream` handles writing automatically, which genuinely reduces code for simple cases. The claim that it is simpler than CSV for basic use is accurate.

**(b)** Significant limitation the AI omitted: Java serialization is brittle across class changes. If you add a field, remove a field, or rename a field after serialized files have been created, the deserialization will fail with an `InvalidClassException` (unless you manually manage `serialVersionUID`). This means saved data from a previous version of the application may become permanently unreadable after any change to the class definition.

**(c)** Comparison paragraph:
Java serialization and CSV both persist object data across application restarts, but they have different trade-offs for a student project. Serialization requires less parsing code but produces binary files that cannot be opened or inspected in a text editor, making debugging difficult — if a save fails silently, you cannot tell by looking at the file. CSV files are human-readable and can be checked in any text editor, which makes debugging significantly easier during development. More importantly, CSV survives class changes: if you add a field to `Book`, you can update the parser to handle old and new lines; with serialization, any class change risks making all previously saved files unreadable without careful version management. For a student project where the class definition is likely to change during development, CSV is the safer and more debuggable choice.

---

**Exercise 10**

**Policy 1 — Strict (abort on any malformed line):**
When a malformed line is encountered, `loadFromFile()` throws an exception or halts immediately. No further lines are processed, and the catalog is left in a partial state (or empty, if the error is caught at the top level).
- Context: medical or financial systems where partial data is potentially worse than no data — a half-loaded medication list could cause a dangerous omission.
- Risk: one corrupt line in a large file makes the entire dataset unavailable. Recovery requires manual file repair.

**Policy 2 — Skip-and-log (lenient with record):**
When a malformed line is encountered, it is logged with the line number and content, then skipped. Processing continues with the next line.
- Context: analytics dashboards or reporting tools where displaying most data is more useful than showing nothing, and a missing record does not create a dangerous inconsistency.
- Risk: silently skipped records may go unnoticed. The user sees a catalog that appears complete but is missing entries.

**Policy 3 — Most lenient (ignore silently):**
When a malformed line is encountered, it is silently discarded with no log entry. Processing continues.
- Context: appropriate only in throwaway data import pipelines where data quality is expected to be poor and completeness is not required.
- Risk: data loss is completely invisible. There is no way to know how much data was dropped or whether the cause is a one-time corruption or a systematic format error.

---

### Tier 3 Answers

**Exercise 11**
The correct startup sequence is:

1. Initialize the catalog objects (e.g., `BookCatalog`, `PatronCatalog`) — create the in-memory containers that will hold entities.
2. Call `loadFromFile()` for each catalog — this populates the in-memory containers with the persisted entities from the previous session. "Populated" in Chapter 5's supply-side vocabulary means that all entities exist in memory and are reachable by ID before any transaction begins.
3. Only after both catalogs are populated is a checkout transaction safe to run.

If `loadFromFile()` has not been called before a checkout is attempted, the `PatronCatalog` and `BookCatalog` are empty. A checkout transaction calls something like `patronCatalog.findById(patronId)`, which returns `null` because no patrons have been loaded yet. Any subsequent operation on that `null` reference throws a `NullPointerException`. The supply-side principle from Chapter 5 — that entities must exist before transactions reference them — is not violated by persistence itself, but by skipping or mis-ordering the load step that restores those entities from disk.

---

**Exercise 12**

**(a)** Hypothesis: The appointments that are missing after restart were created during the session but were never written to the file. State diverges at the moment a new `Appointment` object is added to the in-memory list but `saveToFile()` is not called. This is the proximate cause: the in-memory state and the file state separate at that add operation.

**(b)** The most likely root cause is a save strategy issue — specifically, save-on-exit is being used (or no save strategy exists), and the application was closed in a way that bypassed the exit handler (e.g., force-closed, crashed, or the window was closed without triggering the save event). A serialization error would affect all records equally, not just the ones from the last session. A partial-write failure would be visible as a truncated or corrupted file, not as cleanly missing records. Evidence to look for: open the CSV file and check whether appointments from before the last session are present and those from the last session are absent — this pattern confirms save-on-exit with no save triggered.

**(c)** Set a breakpoint at the line in `saveToFile()` where appointments are written, specifically inside the loop: `writer.write(appointment.toCSV())`. Inspect the size of the `appointments` list at the point the breakpoint is hit. If the list contains only the appointments from previous sessions and not from the current session, confirm that the add operation did not update the list the save method is iterating. If the list does contain all appointments including new ones, the bug is in the write loop or the file path. The confirming value is: list size is smaller than the number of appointments the user created; the ruling-out value is: list size matches the expected total.

---

## Instructor Notes

**Common errors to watch for:**

- **Exercise 2:** Students sometimes claim that objects persist "as long as they are referenced." This confuses garbage collection (which happens during runtime) with process exit (which destroys all memory). Clarify that no JVM memory survives a process exit regardless of references.

- **Exercise 7:** The missing `close()` problem is frequently missed by students who have not yet encountered `try-with-resources`. Both problems must be required for full credit. Watch for students who fix the `close()` but miss the `newLine()` — both bugs would cause data loss in the real application.

- **Exercise 8:** Students often describe atomic rename as "preventing all data loss." Push back: atomic rename prevents file corruption (a half-written file), not data loss from infrequent saves. These are different failure modes.

- **Exercise 10:** Weak answers describe "error handling" generally. Require three distinct policies with named real-world contexts. The key distinction is between failing fast (abort), recording and continuing (skip-and-log), and silent discard — these have meaningfully different production behaviors.

- **Exercise 11:** Students who did not internalize Chapter 5's supply-side model will write vague answers about "loading data before using it." Require the vocabulary: entities, preloading, populated catalog, and the specific null failure from a missing load step.

- **Exercise 12:** The most common weak pattern is identifying the symptom ("appointments are missing") as the root cause. Require them to trace the divergence point and identify whether this is a save strategy issue vs. a serialization issue — these have different fixes.

- **Exercise 13 (Challenge):** Most students default to physical failure scenarios (disk full, power loss). The question specifically asks for a logical corruption scenario — data that was wrong before being written, not data that was written incorrectly. Guide students toward: a mutation that was applied to the wrong object, a concurrent modification during iteration, or an in-memory invariant violation that was then faithfully persisted.

**Suggested point distribution:** Tier 1: 5 pts each. Tier 2: 10 pts each. Tier 3: 15 pts each. Tier 4: 20 pts (rubric-graded).
