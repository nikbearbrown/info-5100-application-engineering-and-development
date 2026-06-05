# Worked Exercises: Recursion

*Chapter 12 of INFO 5100 Application Engineering and Development*

> These exercises follow a research-backed sequence: full worked example → matched practice → completion problem → error-recognition → transfer → interleaved review. Each section builds on the previous. Do not skip ahead.

This chapter is about **recursion**: a method that solves a problem by calling itself on a smaller input until it reaches a **base case** that needs no further recursion. Every recursive method has two parts — a **base case** that stops the recursion, and a **recursive case** that makes progress toward that base case. The chapter's named examples are **computing factorials** (`factorial(n) = n * factorial(n-1)`, base case `factorial(0) = 1`) and the **Fibonacci sequence** (`fib(n) = fib(n-1) + fib(n-2)`, base cases `fib(0)=0`, `fib(1)=1`), with the discipline of **tracing the call stack** to verify behavior. The library project supplies the data: recursion can count or traverse the catalog of `Book` objects, walk a patron's chain of renewals, or compute over a nested structure.

---

## Prerequisites

- You can write and call a Java method that returns an `int` or `long`.
- You understand the runtime call stack: each method call pushes a frame; returning pops it.
- You know the library domain types: a `Catalog` holding `Book` objects, and a `Patron` with `Loan` records.

---

## Part A — Full Worked Example: Recursive Factorial with a Call-Stack Trace

**What this demonstrates:** How a recursive method reduces a problem to a smaller instance of itself, stops at a base case, and produces a result that you can verify by tracing the call stack.

**The problem:** A reservation system charges a fee that depends on `n!` (n factorial). Write `factorial(int n)` recursively, then trace `factorial(4)` through the call stack to confirm it returns 24.

```java
// factorial(0) = 1
// factorial(n) = n * factorial(n - 1)  for n > 0
```

**The solution:**

**Step 1 — Write the base case first.**
```java
public static long factorial(int n) {
    if (n == 0) return 1;          // base case
    ...
}
```
*Why:* The **base case** is the input small enough to answer directly, with no further recursion. Writing it first guarantees the recursion has a stopping point — without it, the calls never end and the stack overflows.
*Check:* `factorial(0)` returns `1` immediately; no recursive call is made.

**Step 2 — Write the recursive case to make progress.**
```java
public static long factorial(int n) {
    if (n == 0) return 1;          // base case
    return n * factorial(n - 1);   // recursive case: smaller input
}
```
*Why:* The **recursive case** must move *toward* the base case. The argument shrinks from `n` to `n - 1` on every call, so a non-negative `n` always reaches `0`. This is the "progress toward the base case" property.
*Check:* Each call's argument is strictly smaller and bounded below by 0 — the recursion terminates.

**Step 3 — Trace the call stack downward (winding).**

| call | evaluates to | waits on |
| --- | --- | --- |
| `factorial(4)` | `4 * factorial(3)` | `factorial(3)` |
| `factorial(3)` | `3 * factorial(2)` | `factorial(2)` |
| `factorial(2)` | `2 * factorial(1)` | `factorial(1)` |
| `factorial(1)` | `1 * factorial(0)` | `factorial(0)` |
| `factorial(0)` | `1` (base case) | — returns |

*Why:* Each recursive call pushes a frame that pauses, holding its `n`, until the smaller call returns. Tracing the winding phase shows the stack growing to depth 5.
*Check:* The deepest frame is the base case `factorial(0)`; the stack does not grow further.

**Step 4 — Trace the unwinding (returning) and compute.**

| returns | computes | value |
| --- | --- | --- |
| `factorial(0)` | base case | `1` |
| `factorial(1)` | `1 * 1` | `1` |
| `factorial(2)` | `2 * 1` | `2` |
| `factorial(3)` | `3 * 2` | `6` |
| `factorial(4)` | `4 * 6` | `24` |

*Why:* As each frame's awaited call returns, the frame finishes its multiplication and pops. The final value bubbles back up to the original caller.
*Check:* `factorial(4)` returns `24`. Matches `4! = 24`.

**Final answer:**
```java
public static long factorial(int n) {
    if (n == 0) return 1;
    return n * factorial(n - 1);
}
// factorial(4) == 24
```

**What made this work:** The central concept is the pairing of a **base case** with a **recursive case that makes progress**. The naive failure is to write the recursive case (`n * factorial(n - 1)`) and forget or mis-state the base case — then `factorial(0)` calls `factorial(-1)`, which calls `factorial(-2)`, forever, and the program dies with a `StackOverflowError`. The base case is what converts an infinite descent into a finite computation.

**Self-explanation prompt:** In your own words, why does the recursion stop, and what exactly would go wrong if you deleted the `if (n == 0) return 1;` line?

---

## Part B — Matched Practice Problem: Recursively Counting Available Books

**Same structure, different surface.** Given a `List<Book> books`, write `countAvailable(List<Book> books, int index)` that recursively counts how many books from position `index` onward have `isAvailable() == true`. The base case is "index past the end of the list"; the recursive case advances `index` by one.

Work the same four steps:
1. Write the base case first (what does `index >= books.size()` return?).
2. Write the recursive case so it makes progress (advance `index`, add 1 only when the current book is available).
3. Trace the winding phase as a call-stack table for a 3-book list where books 0 and 2 are available.
4. Trace the unwinding and confirm the returned count is 2.

**Stuck?** The base case must return `0` (no books left to count). The recursive case returns `(current available ? 1 : 0) + countAvailable(books, index + 1)`.

*Instructor note: No solution is provided for Part B. Write both cases and both trace tables yourself, and confirm termination by checking that `index` strictly increases toward `books.size()`.*

---

## Part C — Completion Problem: Recursive Sum of Late Fees

Goal: write `sumFees(List<Loan> loans, int i)` that recursively totals `loan.getFee()` for every loan from index `i` to the end.

**Step 1 — Write the base case (complete).**
```java
public static double sumFees(List<Loan> loans, int i) {
    if (i >= loans.size()) return 0.0;   // base case: nothing left to add
    ...
}
```
*Why:* The base case stops the recursion when the index runs past the end; it returns the additive identity `0.0`.

**Step 2 — Establish the current element (complete).**
```java
double current = loans.get(i).getFee();
```
*Why:* Each frame handles exactly one element and delegates the rest to a smaller recursive call.

**Step 3 — [BLANK] Write the recursive case that makes progress.**
*Your work here:*
_______________________________________________
*Why (your explanation):*
_______________________________________________

**Step 4 — [BLANK] Show the initial call and the trace for a 2-loan list (fees 1.50 and 0.50).**
*Your work here:*
_______________________________________________
*Why (your explanation):*
_______________________________________________

**Step 5 — Verify (complete).**
For loans with fees `1.50` and `0.50`: `sumFees(loans, 0)` returns `1.50 + sumFees(loans, 1)` = `1.50 + (0.50 + sumFees(loans, 2))` = `1.50 + 0.50 + 0.0` = `2.00`.

**Final answer:**
```java
public static double sumFees(List<Loan> loans, int i) {
    if (i >= loans.size()) return 0.0;
    return loans.get(i).getFee() + sumFees(loans, i + 1);
}
double owed = sumFees(currentLoans, 0);
```

**Self-explanation prompt:** Why does incrementing `i` on each recursive call guarantee the base case is eventually reached, and what would happen if you accidentally recursed with `i` unchanged?

---

## Part D — Error-Recognition Problem

> **Use this section only after completing Parts A–C.**

Goal: compute the n-th Fibonacci number, used to size a fee schedule. The intended definition is `fib(0)=0`, `fib(1)=1`, `fib(n)=fib(n-1)+fib(n-2)`.

**Step 1 — Write the base cases (correct).**
```java
public static long fib(int n) {
    if (n == 0) return 0;
    if (n == 1) return 1;
    ...
}
```

**Step 2 — Write the recursive relation (correct).**
The relation `fib(n) = fib(n-1) + fib(n-2)` is the right recurrence and is mathematically sound.

**Step 3 — ⚠ Compute the whole catalog's fee column by calling naive `fib` per row, for large n.**
```java
public static long fib(int n) {
    if (n == 0) return 0;
    if (n == 1) return 1;
    return fib(n - 1) + fib(n - 2);   // ⚠ recomputes the same subproblems
}
// Called for every row, with n up to ~50, on every catalog refresh:
for (Book b : catalog.getAllBooks()) {
    b.setFeeUnits(fib(b.getTierIndex()));   // tierIndex up to ~50
}
```

**Step 4 — Confirm the values are correct (correct-looking).**
The numbers are right: `fib(10)` is `55`, `fib(20)` is `6765`. The output is accurate.

**Your tasks:**
1. **Identify and explain the error.** The recursion is *correct* but **exponentially redundant**. Naive `fib(n)` recomputes the same subproblems repeatedly: `fib(50)` makes on the order of 2^50 calls because `fib(48)` is recomputed by both `fib(49)` and `fib(50)`, and so on down the tree. For `n ≈ 50` per row over a large catalog, the refresh effectively hangs. Correctness is fine; cost is catastrophic.
2. **Write the corrected Step 3.** Eliminate recomputation with **memoization** (or an iterative bottom-up loop):
```java
private static final Map<Integer, Long> memo = new HashMap<>();
public static long fib(int n) {
    if (n == 0) return 0;
    if (n == 1) return 1;
    Long cached = memo.get(n);
    if (cached != null) return cached;       // reuse, don't recompute
    long result = fib(n - 1) + fib(n - 2);
    memo.put(n, result);
    return result;
}
```
With memoization each `fib(k)` is computed once, turning exponential work into linear.
3. **Name the principle violated.** Avoid **redundant recomputation** in tree recursion: when overlapping subproblems exist (naive Fibonacci), cache results instead of recomputing them. Correct recursion is not enough; it must also make progress *without* repeating work.
4. **Write a test that catches this class.** Instrument `fib` with a call counter and assert that computing `fib(40)` makes at most `O(n)` recursive calls (≈ 40), not the millions the naive version makes. The naive version fails this bound; the memoized version passes.

**Why this error is common:** The recurrence is the textbook definition and the outputs are correct, so the exponential blow-up is invisible for small `n` in a demo and only surfaces at scale.

---

## Part E — Transfer Problem: Recursively Summing a File-System Folder

A backup tool must compute the total byte size of a folder. A folder contains files (each with `sizeInBytes()`) and sub-folders, nested to arbitrary depth. Write `totalSize(Folder folder)` recursively. There is no chapter "file-system" example; the base-case-plus-progress structure is identical to the factorial and sum-fees examples — except the recursion branches into a tree.

Design it: name the base case (a folder with no sub-folders contributes only its files' sizes), the recursive case (add each sub-folder's `totalSize`), and confirm the recursion terminates because each call descends to strictly smaller sub-trees.

**Hint (use only if stuck after 10 minutes):** Sum the direct files, then for each sub-folder add `totalSize(subFolder)`. The base case is implicit: a folder with no sub-folders simply skips the recursive loop and returns its files' total.

**Reflection prompt:**
1. What guarantees this recursion terminates, given the folder tree is finite but you never wrote an explicit `if` for the base case?
2. How is this "tree" recursion different from the "linear" recursion in `factorial`, and which trace (winding/unwinding) becomes a tree rather than a single chain?

---

## Part F — Interleaved Review

**Problem F1.** Write a recursive method `power(int base, int exp)` that computes `base^exp` for `exp >= 0`. State the base case, the recursive case, and trace `power(2, 3)` through the call stack to confirm it returns 8.
*Chapter this draws from: Chapter 12 (Recursion).*

**Problem F2.** A `TableView<Book>` controller is loaded from FXML. The `bookTable` field is annotated `@FXML`. Write the `initialize` method that configures the title column's cell value factory and sets `statusLabel` initial text, and explain why this setup must not go in the constructor.
*Chapter this draws from: Chapter 12's FXML / Scene Builder material (`fx:id`, `@FXML` injection, the `initialize` lifecycle).*

**Problem F3.** You must compute the total fees a patron owes across all their loans. Should you solve it with recursion (`sumFees(loans, 0)`) or a simple iterative `for` loop? Defend your choice on the grounds of clarity, stack depth, and what the data structure looks like.
*Note to instructor: intentionally ambiguous — a flat `List<Loan>` is naturally iterative (no benefit to recursion, and deep lists risk stack depth), whereas a nested/tree structure favors recursion. A strong answer ties the choice to the shape of the data, not to a blanket preference.*

**Closing reflection:** Across F1–F3, which problems genuinely needed recursion (self-similar/tree-shaped data) and which were better as iteration (flat sequences)? Knowing when recursion clarifies versus complicates is the chapter's organizing judgment.

---

## Instructor Notes

**Common errors to watch for:**
- Missing or incorrect base case, so the recursion never stops and throws `StackOverflowError`.
- A recursive case that does not make progress (argument unchanged, e.g., recursing on `n` instead of `n - 1`).
- Exponential recomputation in tree recursion (naive Fibonacci) — correct but unusably slow without memoization.

**Signs a student needs to return to the chapter:**
- The student cannot produce a call-stack trace showing the winding and unwinding phases.
- The student reaches for recursion on flat sequential data where a loop is clearer and avoids deep stacks.

**Scaffolding adjustments:** If a student struggles in Part A, have them trace `factorial(2)` by hand on paper, drawing each stack frame, before writing any code. If a student finishes Part F quickly, ask them to convert the recursive `sumFees` to an iterative loop and articulate the trade-off in stack depth and readability.

**Domain adaptation note:** Replace the library `Loan`/`Book` data with inventory `Product` records (recursively summing nested category sub-totals) or scheduling `Appointment` blocks (recursively walking a chain of follow-ups); the base-case-plus-progress structure is unchanged.
