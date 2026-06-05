# Worked Exercises: Methods, Arrays, and File Objects

*Chapter 2 of INFO 5100 Application Engineering and Development*

> These exercises follow a research-backed sequence: full worked example → matched practice → completion problem → error-recognition → transfer → interleaved review. Each section builds on the previous. Do not skip ahead.

---

## Prerequisites

- You understand the **blueprint-and-building** model: a *class* is a blueprint (inert until instantiated); `new` allocates a block of memory on the **heap** and writes the field values into it; that block is an *object* — one specific *instance* of the blueprint.
- You understand that a **reference** variable is not the object. It is an address — "a sticky note with a street address written on it." The note is not the house. Multiple references can hold the same address and reach the same heap block.
- You can perform a **trace** on paper, distinguishing the **stack** (where local variables and references live) from the **heap** (where objects live), and you accept the Feynman standard: you understand a program when you can predict its output *before* it runs, not after.

---

## Part A — Full Worked Example

**What this demonstrates:** The reference-versus-object distinction made visible — why assigning one reference variable to another (`patronC = patronA`) copies the *reference*, not the *object*, so a change "through" one variable is visible "through" the other.

**The problem:** Predict, by tracing on paper before running, exactly what this prints — and explain *why* in terms of the stack and the heap.
```java
Patron patronA = new Patron("Alice", 34, "LIB-0042");
Patron patronC = patronA;
patronC.age = 99;
System.out.println(patronA.age);
```

**The solution:**

**Step 1 — Instantiate: separate the heap block from the reference**
`new Patron("Alice", 34, "LIB-0042")` allocates one block on the heap holding `name: "Alice" | age: 34 | libraryId: "LIB-0042"`. The variable `patronA` on the stack holds the *address* of that block, not the block.
*Why:* "Now something exists." The constructor populates the heap block; `patronA` is a reference — a sticky note with the block's address. The blueprint was inert until `new`.
*Check:* Draw it. Stack: `patronA ──►`. Heap: `[ name:"Alice" | age:34 | libraryId:"LIB-0042" ]`. One block, one arrow.

**Step 2 — Assign reference to reference: copy the note, not the house**
`patronC = patronA` copies the *address*, not the object. Now two sticky notes carry the same address.
*Why:* "`patronC = patronA` does not copy the object. It copies the reference." No `new` appears on this line, so no new heap block is created.
*Check:* Update the trace. Stack: `patronA ──►` and `patronC ──►` both arrow to the *same* heap block. There is still exactly one block.

**Step 3 — Write through one reference: follow the note, change the block**
`patronC.age = 99` follows `patronC`'s address to the shared block and writes `99` into the `age` field.
*Why:* Field access follows a reference to a specific heap block and mutates it. Because both notes hold the same address, this is the *only* `Patron` block in existence.
*Check:* Heap now reads `[ name:"Alice" | age:99 | libraryId:"LIB-0042" ]`. Both arrows still point here.

**Step 4 — Read through the other reference: same note destination, changed value**
`patronA.age` follows `patronA`'s address — the same block — and reads `99`.
*Why:* "When you ask for `patronA.age`, you follow a different sticky note to the same block and read the changed value." The two references were never independent.
*Check:* Trace table:

| line | heap `age` | `patronA.age` reads | `patronC.age` reads |
| --- | --- | --- | --- |
| after instantiation | 34 | 34 | — |
| after `patronC = patronA` | 34 | 34 | 34 |
| after `patronC.age = 99` | 99 | 99 | 99 |

**Final answer:**
```
99
```
Most students predict `34` because they imagine `patronC` is a copy. It is not — it is a second note bearing the same address, so the write through `patronC` is visible through `patronA`.

**What made this work:** The central concept is the **reference-versus-object distinction**. A naive approach treats `patronC = patronA` as duplicating the patron, which is wrong: assignment copies the address on the stack, leaving exactly one object on the heap. This is "Java working exactly as designed," and it is the foundational model for every unexpected mutation and every moment two variables seem mysteriously synchronized.

**Self-explanation prompt:** Close the page and write one sentence: what principle did Step 2 rely on, and when would the prediction be different (i.e., what single word added to the `patronC = ...` line would create a *separate* heap block so `patronA.age` stays 34)?

---

## Part B — Matched Practice Problem

**Same structure, different surface.** Trace this on paper before running, predict each line of output, and explain the last line in one sentence using stack-and-heap language:
```java
Patron x = new Patron("Carla", 29, "LIB-0007");
Patron y = x;
y.age = 40;
System.out.println(x.age);
System.out.println(y.age);
Patron z = new Patron("Carla", 29, "LIB-0007");
System.out.println(x == z);
```
Produce a trace table showing the heap blocks and which references point where, then a Final answer with all three printed lines.

**Stuck?** Return to Part A and map each step to your obstacle — especially Step 2 (reference-to-reference copy) for the `y = x` line, and notice that `z` uses `new`, which is the difference that drives the `x == z` result.

*Instructor note: No worked solution provided for Part B — the point is production, not verification.*

---

## Part C — Completion Problem

**What's missing:** Steps 3 and 4 are removed.

**The problem:** Predict the output, tracing before running:
```java
Patron p = new Patron("Dana", 40, "LIB-0100");
Patron q = new Patron("Dana", 40, "LIB-0100");
Patron r = q;
r.age = 65;
System.out.println(p.age);
System.out.println(q.age);
```

**Step 1 — Instantiate two independent blocks (complete)**
`new` runs twice, so the heap holds **two** separate blocks, each `[ name:"Dana" | age:40 | libraryId:"LIB-0100" ]`. `p` arrows to the first, `q` to the second.
*Why:* "Java does it again. Another block of memory on the heap." Identical field values do not make them the same object; each `new` builds a distinct instance.

**Step 2 — Alias the second block (complete)**
`r = q` copies `q`'s address. Now `q` and `r` are two notes holding the same address — both point at the second block. `p` is untouched.
*Why:* Reference-to-reference assignment copies the note, not the house; no `new`, so no third block.

**Step 3 — [BLANK] Write through `r` and update the trace table**
*Your work here:*
_______________________________________________
_______________________________________________
*Why (your explanation):*
_______________________________________________

**Step 4 — [BLANK] Read `p.age` and `q.age`; predict both printed values**
*Your work here:*
_______________________________________________
_______________________________________________
*Why (your explanation):*
_______________________________________________

**Step 5 — Verify against a run (complete)**
Run the program and compare to your trace. If the output differs from your prediction, you have a specific question — *where did my model break?* — which is far more tractable than generic confusion.
*Why:* This is the chapter's trace-before-run discipline: the trace makes the invisible reference relationships visible before execution hides them again.

**Final answer:**
```
40
65
```
`p` points at the first block (never modified, age 40); `q` and `r` share the second block, where `r.age = 65` is visible through `q`.

**Self-explanation prompt:** Compare your Steps 3–4 to Part A's Steps 3–4. In Part A there was one shared block; here there are two blocks and only one is shared. What single line in this program is the reason `p.age` is unaffected while `q.age` changes?

---

## Part D — Error-Recognition Problem

> **Use this section only after completing Parts A–C.**

**What's wrong:** one error, marked ⚠.

**The problem:** A method should decide whether two patron references describe the *same person's record* — same name, same library ID — regardless of whether they are the same object in memory.
```java
public boolean sameRecord(Patron a, Patron b) {
    // ... compare the two patrons ...
}
```

**Step 1 — (correct) State what "same record" means**
"Same record" means the two patrons have equal field values (same `name`, same `libraryId`) — content equality — not necessarily the same heap block.
*Why correct:* Distinguishes content equality from reference identity, the chapter's `==`-vs-`equals()` theme.

**Step 2 — (correct) Recognize there may be two distinct objects**
The two arguments may be two separate heap blocks built by two `new` calls that happen to carry identical field values, so they are different objects with the same content.
*Why correct:* Matches the chapter: two objects from one blueprint can hold the same values yet live in different blocks.

**Step 3 ⚠ — Compare the two patrons**
```java
return a == b;
```
The method uses `==` to decide whether the records are the same.
*Why it looks fine:* In a quick test where the caller passes the *same* reference twice (`sameRecord(p, p)`), `==` returns `true`, producing a plausible-looking pass.

**Step 4 — (correct, and that is what makes it dangerous) Observe a passing demo**
The student tests with `sameRecord(patronA, patronC)` where `patronC = patronA`, sees `true`, and concludes the method works.
*Why this is a trap:* `patronC = patronA` is an alias — the same block — so `==` is `true` by accident. With two `new`-built patrons holding identical fields, `==` returns `false` and the method silently reports "different record" when the records are in fact the same.

**Your tasks:**
1. **Identify and explain the error.** Step 3 uses `==`, which "tests reference equality — whether two variables point to the same heap block." The requirement is *content* equality. Two distinct objects with identical fields fail `==`.
2. **Write the corrected Step 3.** Use a properly overridden `equals()` for content comparison:
```java
return a.equals(b);   // requires Patron to override equals() on name + libraryId
```
3. **Name the principle violated.** `==` compares references (heap addresses); content equality requires `equals()`. Java does not make `==` do content equality by default — for objects, `==` is identity.
4. **Describe a test to catch this class of error.** Build two patrons with `new` using identical field values (not an alias), call `sameRecord`, and assert `true`. The `==` version returns `false` and fails; the `equals()` version passes. Also test two patrons with different fields to assert `false`.

**Why this error is common:** `==` compiles and appears correct whenever the caller happens to pass aliased references (a copied note pointing at one block), so the reference-identity bug hides until two genuinely distinct objects with equal content are compared — exactly the shared-reference trap the chapter centers on, inverted.

---

## Part E — Transfer Problem

**Same principle, new context.** Leave patrons behind. In a music app you have a `Playlist` class with a field `List<String> songs`. A user does:
```java
Playlist weekday = new Playlist();
Playlist weekend = weekday;     // "I want a separate playlist for the weekend"
weekend.songs.add("Africa");
```
The user is shocked that "Africa" now appears on their weekday playlist too. Without being given the chapter's `Patron` example, (1) explain in stack-and-heap terms why both playlists changed, (2) draw the trace, and (3) state what the user must do instead to get two genuinely independent playlists. You do not need to write a full deep-copy implementation — describe what has to happen.

**Hint (use only if stuck after 10 minutes):** The chapter's reference-versus-object model is domain-independent. Ask: how many times did the word `new` appear? That number is how many heap blocks exist — and the assignment that lacks `new` is the one that copied a note rather than a house.

**Reflection prompt:** (1) Which chapter concept did you apply, and how did you recognize it transferred from patrons to playlists? (2) What was different here compared to Part A — and what stayed exactly the same about the reasoning?

---

## Part F — Interleaved Review

**Mixed problem set.** Decide which concept applies before solving — that selection is the point.

**Problem F1:** Write a `Book` class with `title`, `author`, `isbn`, and `yearPublished`, plus a constructor and a `toString()` override. Instantiate three distinct books, print each, then change one book's `title` and confirm by tracing that the other two are unaffected. Explain in stack-and-heap terms why they are unaffected. *Chapter this draws from: Chapter 2 (Methods, Arrays, and File Objects).*

**Problem F2:** Given a `Book` class and its `checkOut()` behavior, a checkout call compiles and runs, marks the book unavailable, but the patron's borrowed list never gains the book — no exception is thrown. Name which of the *three kinds of wrong* this is and how you would detect it. *Chapter this draws from: Chapter 1 (Fundamentals of Programming in Java) — the three kinds of wrong.*

**Problem F3:** Two `Book` variables print identical output from their `toString()`. A teammate concludes "they must be the same book, so `==` will be `true`." This *looks* like a simple display question, but it is really a reference-identity question (this chapter), which can be confused with the content-vs-meaning verification from the previous chapter. Decide whether identical `toString()` output guarantees `==` is `true`, justify it with the blueprint/heap model, and name the one operator or method that actually settles each interpretation. *Note to instructor: intentionally ambiguous; commit to an approach, then reflect.*

**After F1–F3:** State which concept you reached for first in each — especially F3, where the right reach is the reference-versus-object model (identical `toString()` does not imply identical reference), not a verification-against-requirement question from the prior chapter.

---

## Instructor Notes

**Common errors to watch for:**
- Students believe `b = a` (without `new`) creates a second object; they predict `34` in Part A and are surprised by `99`. Re-anchor on "how many `new` calls = how many heap blocks."
- Students compare objects with `==` expecting content equality (Part D); surface this by passing two `new`-built objects with identical fields rather than an alias.
- Students skip the trace and reason from the printout, which shows values but never references — the invisible relationship the chapter insists they draw.

**Signs a student needs to return to the chapter:**
- They cannot draw a stack/heap diagram distinguishing references from heap blocks for a two-object program.
- They cannot predict output *before* running and only say "oh, of course" after seeing it — the Feynman standard the chapter sets.

**Scaffolding adjustments:** *For students who struggle with Part A:* give them the partially drawn diagram (the heap block already drawn) and ask only "how many arrows point at this block after `patronC = patronA`?" — isolate the aliasing before the write. *For students who finish Part F quickly:* have them attempt the chapter's Challenge — implement a correct `equals()` override for their domain class and test it against three cases (same object, equal-content distinct objects, different-content objects), explaining why `==` is not content equality by default.

**Domain adaptation note:** Books, inventory items, and clinic appointments are all just blueprints producing heap objects reached by references — the stack/heap trace and the `==`-vs-`equals()` distinction are identical regardless of which domain noun the class is named after.
