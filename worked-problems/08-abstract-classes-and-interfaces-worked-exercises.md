# Worked Exercises: Abstract Classes and Interfaces

*Chapter 8 of INFO 5100 Application Engineering and Development*

> These exercises follow a research-backed sequence: full worked example → matched practice → completion problem → error-recognition → transfer → interleaved review. Each section builds on the previous. Do not skip ahead.

---

## Prerequisites

- You can write a Java class with an array of objects and a `count` field, and you can read and write text files with `BufferedReader`/`BufferedWriter` and `FileReader`/`FileWriter`.
- You understand the chapter's lifecycle: **persistence** means data survives the process; the full path is **object → file → object** via a **save** (writer) and a **load** (reader).
- You can name the four **CRUD** operations (Create, Read, Update, Delete) and the chapter's three policy questions: *what if the write fails, what if the file is missing, how much data loss is acceptable?*

---

## Part A — Full Worked Example

**What this demonstrates:** Adding CSV **persistence** to the catalog so books survive a restart — a writer method, a reader method, call sites, and **exception handlers** that implement explicit decisions about each failure mode.

**The problem:** The library catalog stores `Book` objects in an in-memory array. You enter books, the program works, you close it — and on restart the catalog is empty. Memory is temporary; the books were never written anywhere. Make them survive. A CSV line is one book:

```
Thinking in Java,Bruce Eckel,978-0-131-87248-6,true
Effective Java,Joshua Bloch,978-0-134-68599-1,true
Clean Code,Robert Martin,978-0-132-35088-4,false
```

**The solution:**

**Step 1 — Answer the three policy questions before writing code.** Write one sentence each:
- *What if the write fails?* Log the error and warn the user; do not overwrite a good file with a partial one.
- *What if the file is missing?* On first run, start with an empty catalog (not an error); after established use, this should be flagged.
- *How much data loss is acceptable?* For this learning project, one session — save on exit.

*Why:* The chapter's phase gate: the policy answer *determines the code*. Getting the code right without making the decision means the code makes the decision for you, and you may not like what it decided.
*Check:* Each answer names a *specific behavior*, not a vague intention.

**Step 2 — Write the writer method (serialize objects to CSV).**

```java
public void saveToFile(String filename) throws IOException {
    BufferedWriter writer = new BufferedWriter(new FileWriter(filename));
    for (int i = 0; i < count; i++) {
        Book b = books[i];
        writer.write(b.getTitle() + "," + b.getAuthor() + "," +
                     b.getIsbn() + "," + b.isAvailable());
        writer.newLine();
    }
    writer.close();
}
```

*Why:* The **writer method** is the object→file transition: it serializes each in-memory `Book` to one CSV line. This is the **save** that makes the data persistent.
*Check:* After calling it, open the file in a text editor — every book appears as one comma-separated line.

**Step 3 — Write the reader method with explicit exception handlers.** This is where the policy answers from Step 1 become code.

```java
public void loadFromFile(String filename) {
    File f = new File(filename);
    if (!f.exists()) {
        return;                                  // policy: missing file = start empty, not an error
    }
    try {
        BufferedReader reader = new BufferedReader(new FileReader(f));
        String line;
        while ((line = reader.readLine()) != null) {
            String[] parts = line.split(",");
            if (parts.length < 4) {              // policy: malformed line = skip and log
                System.err.println("Skipping malformed line: " + line);
                continue;
            }
            try {
                String title = parts[0];
                String author = parts[1];
                String isbn = parts[2];
                boolean available = Boolean.parseBoolean(parts[3]);
                addBook(new Book(title, author, isbn, available));
            } catch (Exception e) {              // policy: parse failure = skip record, log
                System.err.println("Could not parse line: " + line);
            }
        }
        reader.close();
    } catch (IOException e) {                     // policy: IO failure = log, accept partial catalog
        System.err.println("Failed to load catalog: " + e.getMessage());
    }
}
```

*Why:* The **exception handlers** are not boilerplate — they *are* the design. Each branch implements one policy decision: missing file → start empty; malformed line → skip and log; IO failure → log and accept a partial catalog.
*Check:* Map each handler to a row:

| Failure mode | What naive code does | This code's response | Policy decision |
| --- | --- | --- | --- |
| Missing file (first run) | crashes / FileNotFound | `return;` empty catalog | not an error |
| Malformed line (<4 fields) | ArrayIndexOutOfBounds | skip + log, continue | tolerate bad rows |
| Parse failure on a field | exception propagates | skip record + log | tolerate bad records |
| IO failure during read | propagates, crashes | catch + log, partial load | accept partial |

**Step 4 — Place the call sites in the application lifecycle.**

```java
public static void main(String[] args) throws IOException {
    Catalog catalog = new Catalog(100);
    catalog.loadFromFile("catalog.csv");          // call site: load at startup
    // ... session: add books, check out, update ...
    catalog.addBook(new Book("Clean Code", "Robert Martin", "978-0-132-35088-4", false));
    catalog.saveToFile("catalog.csv");            // call site: save on exit (per policy)
}
```

*Why:* The **call sites** are the third artifact. A writer and reader that are never called are methods that do nothing; the call sites place them at the right moments per the data-loss policy (here, save on exit).
*Check:* Comment out the `saveToFile` call and restart — the new book is gone. Restore it — the book survives. The call site is load-bearing.

**Step 5 — Verify the full lifecycle and find the data-loss window.** Add three books, exit, restart, confirm all three load. Then deliberately place `System.exit(0)` *after* a mutation but *before* `saveToFile`. Restart: the mutation is gone.
*Why:* This exposes the **data-loss window** — the interval between an in-memory change and the file write. The interrupted transition is object→file (the save never ran).
*Check:* Expected behavior — books added before the last successful save survive; anything changed after it does not. The record does not match the world only across that window.

**Final answer:** Four artifacts present — writer (`saveToFile`), reader (`loadFromFile`), call sites (load at startup, save on exit), and exception handlers (one explicit decision per failure mode). The catalog survives restart; the three policy questions are answered in writing and reflected in the code.

**What made this work:** The central concept is that **persistence transforms each CRUD operation from trivial to consequential** — and that the **exception handlers are the design, not boilerplate**. The naive approach — declaring `throws IOException` and letting the caller worry, or wrapping everything in a try-catch that swallows errors until the compiler stops complaining — fails because it *defers the decision*. The compiler accepts silent swallowing; the user does not accept losing an hour of work because nobody decided what to do when the disk was full or the file was missing.

**Self-explanation prompt:** In your own words, why is "a missing file" sometimes the correct, expected condition (first run) and sometimes a serious error (after months of use) — and why can't the code alone decide which?

---

## Part B — Matched Practice Problem

**The problem:** Add CSV persistence to an inventory system whose `ProductCatalog` holds `Product` objects (name, SKU, stock, active flag) in an array with a `count` field. Produce: (1) the three policy answers in writing — what if the write fails, what if the file is missing, how much data loss is acceptable; (2) a `saveToFile` writer that serializes each product as a CSV line; (3) a `loadFromFile` reader with explicit exception handlers for missing file, malformed line (fewer than 4 fields), parse failure, and IO failure — each commented with the policy it implements; (4) the call sites in `main` (load at startup, save per your policy); (5) a restart verification plus a deliberate `System.exit(0)` test that exposes the data-loss window, with the expected result.

**Stuck?** Map every line of your reader to one of the four failure-mode rows. Any failure mode without a corresponding handler is a place your program will crash or silently lose data on the first file-system anomaly.

*Instructor note: No solution is provided for Part B. Write the three policy answers before any code, then implement the four artifacts. The structure deliberately mirrors Part A in the inventory domain.*

---

## Part C — Completion Problem

**The problem:** Add CSV persistence to a healthcare scheduling system whose `ApptStore` holds `Appointment` objects (id, patientId, providerId, kept-flag) in an array. Because a missing appointment record could affect patient care, the data-loss policy is stricter than the library's.

**Step 1 — Answer the three policy questions.**
- *What if the write fails?* Log and warn the user; never overwrite a good file with a partial one.
- *What if the file is missing?* On first run, start empty; after established use, refuse to overwrite with an empty store and alert.
- *How much data loss is acceptable?* Zero tolerance for the last transaction — save after every mutation.

*Why:* The stricter policy (save after every mutation) follows from the domain's stakes; the chapter says the answer determines the code.

**Step 2 — Write the writer method.**

```java
public void saveToFile(String filename) throws IOException {
    BufferedWriter writer = new BufferedWriter(new FileWriter(filename));
    for (int i = 0; i < count; i++) {
        Appointment a = appts[i];
        writer.write(a.getId() + "," + a.getPatientId() + "," +
                     a.getProviderId() + "," + a.isKept());
        writer.newLine();
    }
    writer.close();
}
```

*Why:* The **writer method** serializes each appointment to one CSV line — the object→file transition.

**Step 3 — [BLANK] Write the reader method with explicit exception handlers.**
*Your work here:* ________________________________________________
(Check `f.exists()` first — start empty if missing; loop lines; skip lines with fewer than 4 fields and log; wrap field parsing in a try-catch that logs and skips; wrap the whole read in a try-catch on `IOException`.)

*Why (your explanation):* ________________________________________________

**Step 4 — [BLANK] Place the call sites per the every-mutation policy.**
*Your work here:* ________________________________________________
(Load at startup in `main`; call `saveToFile` after *every* mutation — every add, cancel, and update — not just on exit.)

*Why (your explanation):* ________________________________________________

**Step 5 — Verify and find the data-loss window.** Add an appointment, confirm it persisted by restarting. Then place `System.exit(0)` after a mutation but before the save would run under a save-on-exit design; observe that with save-after-every-mutation the window shrinks to near-zero.
*Why:* The save strategy directly sets the size of the data-loss window; the stricter healthcare policy is what closes it.

**Final answer:** Four artifacts — `saveToFile` (writer), `loadFromFile` (reader with explicit handlers), call sites (load at startup, save after every mutation), exception handlers (one decision per failure mode). Policy answers written first; the zero-tolerance window drives save-after-every-mutation.

**Self-explanation prompt:** Explain why the *same* writer and reader code can serve very different data-loss guarantees depending only on *where* the save call site is placed.

---

## Part D — Error-Recognition Problem

> **Use this section only after completing Parts A–C.**

A student adds persistence to the library catalog. Their write-up:

**Step 1 (correct).** Policy answers written: missing file → start empty; data loss → save on exit.

**Step 2 (correct).** `saveToFile` serializes each book to a CSV line and is called on exit.

**Step 3 ⚠.** "For `loadFromFile` I wrapped the entire body in one big try-catch that catches `Exception` and does nothing in the catch block: `try { ... } catch (Exception e) { }`. This way the program never crashes no matter what is in the file — missing file, malformed line, bad field, anything. Since it never crashes, persistence is robust and the lifecycle is complete."

**Step 4 (correct-looking).** The student adds three books, exits, restarts. The books load. The demo passes — no crash, books present — a plausible-looking result.

**Your tasks:**

1. **Identify and explain the error in Step 3.** Catching `Exception` with an empty body *silently swallows* every failure. The compiler accepts it, but it erases the design: a malformed line, a missing file, and a disk error now all produce the *same* invisible non-response. When a future file is half-corrupt, the load will silently stop partway and the catalog will be quietly incomplete — with no log, no warning, and no way for the user to know data was lost. "It never crashes" is not robustness; it is the chapter's named failure mode — handling the exception by catching and continuing without deciding what each failure *means*.

2. **Write the corrected Step 3.** Replace the blanket catch with the chapter's explicit handlers: check `f.exists()` and return empty if missing (not an error); skip and *log* lines with fewer than four fields; wrap field parsing in its own try-catch that logs and skips the record; catch `IOException` around the read and log, accepting a partial catalog. Each branch is a *decision*, and each logs so the loss is visible.

3. **State the principle violated.** Exception handling is not "add try-catch until the compiler stops complaining" — it is deciding, for each failure mode, what the correct behavior is and implementing it explicitly. A silent empty catch defers (and hides) every decision.

4. **Design a test to catch this class of error.** Deliberately corrupt the CSV — remove a field from one line and add a junk line — then load. With the correct handlers, the load logs exactly which lines it skipped and loads the rest; with the empty catch, the load silently produces a smaller catalog and prints nothing. The test asserts that every skipped/failed record produces a log line, so silent loss is impossible to miss.

**Why this error is common:** "The program never crashes" feels like success, so students equate *not throwing* with *handling*, swallowing exceptions silently instead of deciding what each failure should do.

---

## Part E — Transfer Problem

**The problem (different domain — a personal expense tracker, not the chapter's library/inventory/scheduling trio):** An `ExpenseLog` holds `Expense` objects (date, category, amount, cleared-flag) in an array. The user enters expenses, the program works, and on restart everything is gone. Add CSV persistence: write the three policy answers (what if the write fails, what if the file is missing, how much data loss is acceptable — note that for financial records the tolerance is low), a `saveToFile` writer, a `loadFromFile` reader with explicit exception handlers (missing file, malformed line, parse failure, IO failure), call sites at startup and per your policy, and a restart test plus a `System.exit(0)` test that exposes the data-loss window.

**Hint (use only if stuck after 10 minutes):** Map the four artifacts directly: `saveToFile`=writer, `loadFromFile`=reader, the `main` load/save lines=call sites, the per-failure-mode branches=exception handlers. The CSV format is one expense per line; the policy questions are identical — only the *answers* change because money is involved.

**Reflection prompt:** (1) What made it possible to transfer the catalog persistence design to an expense tracker with no new file-I/O concepts? (2) Which single policy answer changes most because the data is financial rather than a book list, and how does that change the placement of the save call site?

---

## Part F — Interleaved Review

**Problem F1.** Your catalog uses save-on-exit. A book is checked out (availability flag flipped in memory) and the program crashes before the save runs. On the next start, the book loads as available. Name the interrupted lifecycle transition, the size of the data-loss window, and the one policy change that would have prevented it.
*Chapter this draws from: Chapter 8 (Abstract Classes and Interfaces — persistence lifecycle, data-loss window, save strategies).*

**Problem F2.** A `Catalog` of `Book` entities is preloaded in `main` before any patron exists, and a checkout queries it with `findByIsbn`. Run the separation test in prose: with all checkouts commented out, is the catalog still queryable, and what does that prove about the supply side?
*Chapter this draws from: Chapter 5 (Inheritance and Polymorphism — entity, collection class, query method, separation test).*

**Problem F3 (discrimination).** A program loads a catalog from `catalog.csv` at startup, the user updates a book's title in memory, and on restart the title is unchanged. A student says "this is a persistence bug — the reader must be parsing wrong." Decide whether the defect is a persistence/exception-handling problem (Chapter 8) or a stale-in-memory-vs-file causal-diagnosis problem (Chapter 4), and justify which method to apply first.
*Note to instructor: intentionally ambiguous — the surface cue ("persistence," "csv," "reader") points at Chapter 8, but if the writer and reader are correct and the issue is that `saveToFile` was never called after the update (the data-loss window), the diagnosis is a missing-call-site / stale-state problem best attacked with Chapter 4's hypothesize-isolate-test before rewriting any parsing code.*

**After F1–F3:** Write two sentences naming the cue that pulled you toward the wrong chapter in F3 and how you decided which method to apply first.

---

## Instructor Notes

**Common errors to watch for:**
- A single blanket `catch (Exception e) {}` that silently swallows every failure (the Part D error), mistaking "never crashes" for "handled."
- Treating a missing file on first run as a fatal error (crash) rather than the expected empty-catalog condition.
- Writing correct `saveToFile`/`loadFromFile` methods but omitting or misplacing the call sites, so updates live only in memory and vanish across the data-loss window.

**Signs a student needs to return to the chapter:**
- They cannot state, for their own code, the answers to the three policy questions, or those answers are not reflected in any exception handler.
- They cannot point to all four artifacts (writer, reader, call sites, exception handlers) and explain what is lost if any one is missing.

**Scaffolding adjustments:** If a student struggles with Part A, have them complete only the failure-mode table (Step 3 *Check*) first — matching each row to a specific branch in `loadFromFile` makes the handlers concrete before they write them. If a student finishes Part F quickly, have them design the `saveIfDirty` / dirty-flag optimization (Challenge exercise) and name what it buys, what it costs, and the new failure mode it introduces.

**Domain adaptation note:** Swap the `Book`/`Catalog` CSV for the student's project records (products, appointments, expenses) — the object→file→object lifecycle, the four artifacts, and the three policy questions are identical across domains; only the field layout of each CSV line and the *answers* to the data-loss question change.
