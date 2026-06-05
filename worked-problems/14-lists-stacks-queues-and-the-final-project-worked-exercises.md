# Worked Exercises: Lists, Stacks, Queues, and the Final Project
*Chapter 14 of INFO 5100 Application Engineering and Development*

> These exercises follow a research-backed sequence: full worked example → matched practice → completion problem → error-recognition → transfer → interleaved review. Each section builds on the previous. Do not skip ahead.

## Prerequisites
- You can use the `List` interface and both its implementations, `ArrayList` and `LinkedList`, and you know the `Stack` (LIFO) and `Queue` (FIFO, via `LinkedList`) contracts.
- You can write a `Comparator<Book>` to define an ordering rule and pass it to `sort` or a `PriorityQueue`.
- You understand the layered semester project: supply side (`Book`, `Author`, `Catalog`), transaction layer (`CheckoutTransaction`, `PatronSession`), persistence, view (`ListView`, `Button`, `Label`), and event handlers.

---

## Part A — Full Worked Example: An undo history for checkout actions using a Stack

**What this demonstrates:** Choosing the LIFO `Stack` contract for an undo feature, and why peeking or popping an empty stack must be guarded.

**The problem:** The GUI needs an "Undo last checkout" button. Each successful `controller.performCheckout()` should be recorded so the most recent one can be reversed first. A teammate stored the history in an `ArrayList<CheckoutTransaction>` and "undid" by reading index 0:

```java
List<CheckoutTransaction> history = new ArrayList<>();
// after each checkout:
history.add(tx);
// undo handler:
CheckoutTransaction last = history.get(0);   // "the first one"
history.remove(0);
last.reverse();
```

It runs. But it undoes the *oldest* checkout, not the most recent, and on an empty history `history.get(0)` throws `IndexOutOfBoundsException`. We need correct most-recent-first behavior.

**The solution:**

**Step 1 — Name the contract the feature requires.** "Undo the most recent action first" is *last-in, first-out* — the `Stack` (LIFO) contract.
*Why:* The data structure must encode the access rule. Undo always touches the newest item; that is the definition of LIFO. Choosing the structure by its contract, not by familiarity, is the move.
*Check:* Say it aloud: "most recent out first" = LIFO = `Stack`. If you had said "oldest out first," that would be FIFO = `Queue`.

**Step 2 — Explain why the `ArrayList` version is wrong.** `history.get(0)` returns the *first* element added (the oldest), and `add` appends to the end, so index 0 is the front of a FIFO order, not the top of a LIFO stack.
*Why:* An `ArrayList` has no LIFO/FIFO contract of its own — it is an ordered, index-addressable sequence. Using it as a stack requires you to manually push/pop the *end* (`add` / `remove(size-1)`), and reading index 0 silently implements a queue instead.
*Check:* Trace checkouts A, then B, then C.

| action | structure state (bottom→top) | undo reads | should read |
| --- | --- | --- | --- |
| push A | [A] | — | — |
| push B | [A, B] | — | — |
| push C | [A, B, C] | — | — |
| undo (ArrayList `get(0)`) | removes A | **A (oldest)** | C (newest) |

The mismatch is clear: it undoes A when it should undo C.

**Step 3 — Use the Stack contract directly.**
```java
Stack<CheckoutTransaction> history = new Stack<>();
// after each checkout:
history.push(tx);
// undo handler:
CheckoutTransaction last = history.pop();   // top = most recent
last.reverse();
```
*Why:* `push` adds to the top and `pop` removes the top, so the most recent checkout is always the one reversed. The contract now matches the requirement; no index arithmetic to get wrong.
*Check:* Re-trace A, B, C: `push A`→[A], `push B`→[A,B], `push C`→[A,B,C], `pop`→returns **C**. Correct.

**Step 4 — Guard the empty case.** Pressing Undo with no history must not crash.
```java
if (history.isEmpty()) {
    statusLabel.setText("Nothing to undo.");
    return;
}
CheckoutTransaction last = history.pop();
last.reverse();
```
*Why:* `Stack.pop()` (and `peek()`) on an empty stack throws `EmptyStackException`. The empty case is a real user state — the button exists before any checkout happens — so it must be handled, not assumed away.
*Check:* With `history` empty, the guard fires, the label updates, and `pop()` is never reached. No exception.

**Step 5 — State the trade-off you accepted.** `Stack` is a legacy class synchronized on every operation; for a single-threaded JavaFX handler that overhead is negligible, and the explicit LIFO contract makes the intent self-documenting.
*Why:* A defensible design decision names the alternative (`Deque`/`ArrayDeque` as the modern LIFO choice) and why the requirement made the choice acceptable here (clarity over micro-performance for a small, single-threaded undo history).
*Check:* You can answer the examiner's "why a `Stack` and not an `ArrayList`?" with "LIFO is the requirement; `Stack` encodes it; `ArrayList` does not."

**Final answer:** Back the undo history with a `Stack`, `push` on each checkout, `pop` to undo, and guard `isEmpty()` before `pop`/`peek`; an `ArrayList` read at index 0 silently implements FIFO and crashes when empty.

**What made this work:** The central concept is **matching the structure's contract (LIFO `Stack` vs FIFO `Queue`) to the access requirement**, plus the discipline of guarding empty-structure access. The naive approach fails twice: it confuses LIFO with FIFO (undoing the oldest), and it ignores the empty case (`IndexOutOfBoundsException`) — both invisible in a happy-path demo where you always undo immediately after a checkout.

**Self-explanation prompt:** Explain why an `ArrayList` *can* be made to behave like a stack but a `Stack` *cannot* accidentally behave like a queue — what does the contract buy you?

---

## Part B — Matched Practice Problem: A holds waitlist using a Queue

**What this demonstrates:** Choosing the FIFO `Queue` contract for fairness, and guarding empty access — the mirror image of Part A.

**The problem:** When a book is checked out, other patrons can place a *hold*. When the book is returned, the patron who placed their hold *first* should be offered the book next (first-come, first-served). Write the data structure and the two operations: `placeHold(Patron p)` and `Patron offerToNext()` (returns the next patron in line, or signals empty). A teammate used a `Stack` because "it was in the last example."

Produce a worked solution with the same deep structure as Part A:

**Step 1 — Name the contract the feature requires.** (Is "first to place a hold is served first" LIFO or FIFO?)
**Step 2 — Explain why a `Stack` is wrong here.** (What order would LIFO serve the waitlist in?)
**Step 3 — Use the correct contract directly.** (Which `Queue` operations add to the back and remove from the front? `LinkedList` implements `Queue`.)
**Step 4 — Guard the empty case.** (What do `poll()` vs `remove()` do on an empty queue?)
**Step 5 — State the trade-off you accepted.**

Include a trace table for holds placed by patrons P1, P2, P3 showing who `offerToNext()` returns first.

**Stuck?** Ask: which patron should be served first, the most recent or the earliest? That word — earliest — picks FIFO, and FIFO is the `Queue` contract, not the `Stack` contract.

> Instructor note: No solution is provided for Part B. Work it fully before moving on.

---

## Part C — Completion Problem: Priority return-processing with a Comparator

**What this demonstrates:** Using a `PriorityQueue` with a `Comparator` so returned books are reshelved in a chosen order, not insertion order.

**The problem:** Returned books pile up. They should be reshelved in order of *most overdue first* (largest `getDaysOverdue()` first). Build a structure that, each time you remove an element, hands back the most-overdue book currently waiting.

**Step 1 — Name the access pattern.** "Remove the highest-priority element next, regardless of insertion order" is a *priority queue* pattern, with priority = days overdue (descending).
*Why:* Neither FIFO nor LIFO is correct — order of removal depends on a key, not on arrival time. That is exactly the `PriorityQueue` contract.

**Step 2 — Define the ordering rule as a `Comparator` and create the queue.**
```java
Comparator<Book> mostOverdueFirst =
    (a, b) -> Integer.compare(b.getDaysOverdue(), a.getDaysOverdue()); // b,a = descending
PriorityQueue<Book> reshelf = new PriorityQueue<>(mostOverdueFirst);
```
*Why:* A `PriorityQueue`'s removal order is defined entirely by its `Comparator`; reversing the argument order (`b` before `a`) makes larger overdue counts come out first.

**Step 3 — [BLANK] Add the returned books to the queue.**
*Your work here:*

*Why (your explanation):*

**Step 4 — [BLANK] Remove books in priority order and guard the empty case.**
*Your work here:*

*Why (your explanation):*

**Step 5 — Verify the ordering.** For input days-overdue `{ "A":2, "B":9, "C":0 }`, removing all elements must yield B (9), then A (2), then C (0).
*Why:* This confirms the `Comparator` drives removal order, not insertion order. To verify in a test: poll three times and assert the title sequence is `["B", "A", "C"]`.

**Final answer:** A `PriorityQueue<Book>` constructed with a descending-overdue `Comparator` removes the most-overdue book first regardless of when it was added; you must still guard `poll()` returning `null` on empty.

**Self-explanation prompt:** Why does a `PriorityQueue` *not* keep its elements fully sorted at all times, and why does that not matter as long as each `poll()` returns the current highest priority?

---

## Part D — Error-Recognition Problem: Inserting many books at the front of a reading list

> **Use this section only after completing Parts A–C.**

**The problem:** A patron's "reading list" is built by repeatedly inserting newly recommended books at the *front* (position 0), so the newest recommendation shows on top. A teammate wrote a defense of their data-structure choice. Steps 1, 2, and 4 are correct. One step contains an error.

**Step 1 — Name the access pattern (correct).** "Insert at the front, many times; rarely random-access by index." Front-insertion-dominated.

**Step 2 — Declare the list (correct).**
```java
List<Book> readingList = new LinkedList<>();
```

**Step 3 — ⚠ Justify the choice.**
> "I used a `LinkedList` because `ArrayList` and `LinkedList` perform the same for inserting at the front — both just shift a pointer — so the choice is purely stylistic. I could swap in `ArrayList` with no performance difference."

**Step 4 — Insert at the front (correct).**
```java
readingList.add(0, newBook);   // add at index 0
```

**Your tasks:**
1. Identify the misconception in Step 3's reasoning.
2. Explain the actual cost of `add(0, x)` for `ArrayList` versus `LinkedList`, in terms of what each must do to its internal storage.
3. Rewrite Step 3 as a correct justification that names the trade-off (and says when `ArrayList` *would* be better).
4. Explain why Step 4's code is identical for both implementations even though the performance is not — i.e., why the bug is in the *reasoning*, not the call.

**Why this error is common:** Because `ArrayList` and `LinkedList` share the `List` interface and look interchangeable at the call site, students assume their performance is interchangeable too — forgetting that `ArrayList`'s `add(0, x)` must shift every existing element to make room (linear cost) while `LinkedList`'s only relinks two nodes.

---

## Part E — Transfer Problem: A print spooler for an inventory label printer

**Same principle, new domain.** An inventory system prints shipping labels. Labels are submitted by warehouse staff throughout the day and must print in the exact order submitted (first submitted, first printed) — no label may jump the line. Choose and justify the data structure, write `submit(Label l)` and `Label printNext()`, and guard the empty case. Then state the trade-off you accepted.

Your solution must:
- Name the contract the feature requires (FIFO? LIFO? priority?).
- Choose the matching structure and the implementation that backs it.
- Guard the empty case (no labels waiting).
- State one alternative you rejected and why the requirement ruled it out.

**Hint (use only if stuck after 10 minutes):** "Exact order submitted, no jumping the line" is the same fairness requirement as Part B's holds waitlist — first in, first out. The domain (labels vs holds) changed; the contract did not.

**Reflection prompt:**
1. If management later said "rush orders print first," which structure from Part C would you switch to, and what would you supply to define "rush"?
2. How is this spooler structurally identical to Part B even though one queues patrons and the other queues print jobs?

---

## Part F — Interleaved Review

**Problem F1 (this chapter).** A browser-style "back button" for screen navigation in the JavaFX app must return to the *previous* screen, then the one before that. Choose between `Stack` and `Queue`, write `visit(Screen s)` and `Screen goBack()`, and guard the empty case. State which contract you chose and the one-sentence reason.
*Chapter this draws from: Chapter 14 (Lists, Stacks, Queues).*

**Problem F2 (named previous chapter).** Write a `@Test` that verifies your Part A undo `Stack` enforces its rule: push three checkouts, pop once, and assert the popped transaction is the third (most recent), and assert that a `pop` on an emptied stack is handled without crashing. Name the requirement in plain English before writing the assertions.
*Chapter this draws from: Chapter 13 — Collections and the testing discipline (`@Test`, assertions, the empty/edge-case taxonomy).*

**Problem F3 (discrimination).** You are given three requirements: (a) "undo the last action," (b) "serve patrons in the order they arrived," (c) "reshelf the most overdue book first." For each, state which structure you would choose — `Stack`, `Queue`, or `PriorityQueue` — and the one-sentence reason. Then explain how you decided: which word in each requirement ("last," "order they arrived," "most overdue") drove the choice.
*Note to instructor: F3 forces discrimination among LIFO, FIFO, and priority ordering rather than reflexively reusing the `Stack` from F1.*

**Closing reflection:** Across F1–F3 the recurring question is: does the requirement want the *newest* (LIFO), the *oldest* (FIFO), or the *highest-priority* (priority queue) element next? Name which one each problem needed.

---

## Instructor Notes

**Common errors:**
- Confusing LIFO (`Stack`) with FIFO (`Queue`) — using a stack for a fairness waitlist or a queue for an undo feature.
- Calling `pop()`/`peek()`/`element()` on an empty structure and getting `EmptyStackException` / `NoSuchElementException` instead of guarding with `isEmpty()` or using `poll()`/`peek()` that return `null`.
- Assuming `ArrayList` and `LinkedList` have equal performance for front-insertion or middle-removal, or using a plain `List` where a `Stack`/`Queue` contract was actually required.

**Signs a student needs to return:**
- They cannot state, before coding, whether the next element out should be the newest, the oldest, or the highest-priority.
- They choose `ArrayList` vs `LinkedList` by habit and cannot explain the cost of `add(0, x)` in each.

**Scaffolding adjustments:** If a student struggles with Part A, have them fill the push/pop trace table for A, B, C *before* writing any code, circling which element undo must touch. If a student finishes Part F quickly, have them implement F1's back button with a `Deque`/`ArrayDeque` and defend it against the legacy `Stack` as a final-project design decision.

**Domain adaptation note:** Swap the library undo/holds/reshelf scenarios for inventory print spoolers, restock priority, or scheduling waitlists; the LIFO-vs-FIFO-vs-priority decision and the empty-guard discipline transfer unchanged.
