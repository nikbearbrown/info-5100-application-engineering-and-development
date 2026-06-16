# Module 2 — Methods, Arrays, and File Objects: Wonder Edition
## Companion Chapter

> **Wonder Edition:** Read this alongside the chapter, not instead of it.

> **Content note:** The chapter title lists methods, arrays, and file objects as three parallel topics. The chapter itself teaches one foundational model: the distinction between a reference variable and the heap object it addresses. Methods appear as class-level behavior; arrays and file objects are named in the assessments. The conceptual core — and the core of this companion — is the reference-versus-object model. Read the exercises in the main chapter for the full module scope.

---

## The Strange Question

Two variables are created on separate lines, using identical arguments.

```java
Patron x = new Patron("Carla", 29, "LIB-0007");
Patron z = new Patron("Carla", 29, "LIB-0007");
System.out.println(x == z);
```

The output is `false`.

The variables hold the same name, the same age, the same library ID. Java reports they are not equal. No explanation is offered. The code is not wrong. The behavior is not accidental.

What does `==` actually compare when applied to objects?

---

## First Intuition

The wrong model has a name: the container model. A variable is a box. The box holds the value. When a student writes `patronA.age = 34`, they picture the number 34 sitting inside `patronA`. A second patron is a second box with different contents.

This model comes from arithmetic. In algebra, `x = 5` means the symbol and the number are interchangeable. Wherever `x` appears, 5 substitutes cleanly. The symbol carries the value directly.

The container model handles Java primitives tolerably. An `int` variable does hold its value directly. The model breaks at the moment objects enter — and the break produces bugs that look inexplicable without a replacement model.

> **► Planning prompt:** Before reading further, write your prediction. You have this sequence: `Patron patronC = patronA; patronC.age = 99;`. What does `System.out.println(patronA.age)` print? Write the number down. Write why you expect that number. Do not continue until you have written both.

---

## The Surprise

The container model predicts that `patronC = patronA` copies the patron. Two boxes, two sets of values. Modifying `patronC.age` should leave `patronA.age` untouched.

But `System.out.println(patronA.age)` prints `99`.

The assignment did not copy the patron. `patronA` and `patronC` now reach the same object. A mutation through one name appears when reading through the other.

The `x == z` case cuts the opposite direction. Two variables built from identical arguments evaluate to `false` under `==`. Java created two separate data blocks with matching contents. The `==` test asked whether the two variables point to the same block — they do not.

The container model cannot account for either result. It predicts that `patronC = patronA` separates two values; it predicts that identical inputs imply equality. Both predictions are wrong. The container model does not merely simplify Java's behavior — it contradicts it.

> **► Monitoring prompt:** Stop and write. Do you have a revised model that explains both results at once — the shared mutation and the false equality? If your explanation only covers one of them, or requires a separate rule for each, the model is still incomplete. Identify which assumption your model still fails.

---

## The Hidden Structure

Therefore, Java stores objects and references in separate locations, and a variable holds the location — not the data.

When `new Patron(...)` executes, Java allocates a block of memory on the heap — the region reserved for object data. It writes the field values into that block. The block is the object. That block sits at a specific address in RAM.

The variable on the left does not hold the field values. It holds the address of the heap block. This is the reference: a stored address that points to where the object lives.

```
Stack                  Heap
------                 ------
patronA  ──────────►  [ name: "Alice"   | age: 34 | libraryId: "LIB-0042" ]
patronB  ──────────►  [ name: "Bernard" | age: 51 | libraryId: "LIB-0091" ]
```

The stack holds references. The heap holds objects. The arrow represents the actual address stored in the variable, not a pedagogical decoration.

When `patronC = patronA` executes, Java copies the address from `patronA` into `patronC`. Two stack variables now hold the same heap address. Two arrows point at one block. Every read or write through either name reaches the same data. When `patronC.age = 99` executes, Java follows the address, arrives at the block, and writes 99. When `patronA.age` is read, Java follows its address — the same address — and reads 99.

When `x = new Patron(...)` and `z = new Patron(...)` execute on separate lines, Java creates two separate heap blocks even if the field values match. The `==` operator compares addresses. Different blocks have different addresses. `x == z` is `false` regardless of the contents because the addresses differ.

> "It is tempting to think that `==` checks whether two objects contain the same data — same name, same age, same ID. But `==` on reference types checks only whether two variables store the same memory address. The correct model holds that two variables with identical field values can fail `==`, and two variables with different names can pass it, depending entirely on whether they were assigned the same address. The key distinction is between identity — are these the same physical object in memory? — and equality — do these objects contain equivalent data? Java's `==` answers only the identity question."

**Code Trace — shared reference:**

```java
Patron patronA = new Patron("Alice", 34, "LIB-0042"); // heap block A created; patronA holds address A
Patron patronC = patronA;                              // patronC receives address A; no new block created
patronC.age = 99;                                      // Java follows address A, writes 99 to age field
System.out.println(patronA.age);                       // Java follows address A, reads 99
// Output: 99
```

---

## Try Looking At It This Way

**Target:** Java reference variables and heap objects

**Base:** A library catalog system with physical books and catalog cards

**Features:**
- A catalog card holds a shelf address, not the book's contents — a reference variable holds a heap address, not field values
- Two catalog cards can list the same shelf location — two reference variables can hold the same heap address
- Two physical books can contain identical text while sitting on different shelves — two heap objects can hold identical field values while existing at different addresses

**Commonalities:**
- The card-to-book relationship maps to the reference-to-object relationship because in both cases the locator (card, variable) and the located thing (book, object) are physically separate entities. Modifying the book does not modify the card; modifying the heap block does not modify the reference variable.
- Two cards pointing to one book lead to shared mutation because there is one physical object being reached by two paths — the same reason two references pointing to one heap block produce aliasing.
- Two books with identical content are distinct physical objects because each occupies a unique location in space — the same reason two heap objects created with `new` have distinct addresses even when their fields match.

**Boundaries:** The catalog analogy treats cards as persistent physical objects that can be filed and retrieved across time. Java reference variables are scoped to the method or block that declares them. When that scope ends, the reference variable disappears. The heap object may survive if other references point to it; it becomes eligible for garbage collection if none do.

**Conclusions:** The catalog model makes the stack-heap split concrete and gives a physical intuition for aliasing. It breaks on the question of variable lifetime, which requires tracking scope rather than physical persistence.

---

## Where The Analogy Breaks

> "Unlike a library catalog card, a Java reference variable does not persist beyond the scope that declares it. This matters because the analogy suggests that once a reference is created, it endures as a stable record of the object's location. In Java, a reference variable exists only while its declaring method or block is executing. An object can outlive all references to it — briefly, until garbage collection — but a reference cannot outlive its scope. Reasoning about object lifetimes requires tracking active scopes, not just which references were ever assigned."

---

## Small Discovery

Here is raw data. Resist explanation — look for the pattern first.

A shipping company assigns unique tracking numbers to every package. Two packages leave the same warehouse on the same morning. They carry identical items, identical weight, identical destination. A customer calls to ask whether tracking number A and tracking number B are the same package. The system compares the two tracking numbers. They differ. The system reports: not the same package.

The customer argues: everything about these packages is identical. The contents, the origin, the destination. How can the system say they are different?

> **► Prediction prompt:** What criterion is the tracking system using to define "same"? Is that criterion correct for the company's operational purpose? Write your answer before reading the next paragraph.

---

The tracking system uses identity, not content. Two different tracking numbers represent two physical packages in two physical locations — two trucks, two warehouse bays, two doorsteps. The company's operations depend on knowing which specific package is where. Identical contents do not help locate a specific object in physical space. For the company's purpose, identity is the correct criterion.

This is precisely Java's `==` on objects. The operator asks about identity: are these the same object at the same memory address? Identical field values do not collapse two distinct heap blocks into one. The customer's frustration — expecting content comparison and receiving identity comparison — mirrors the programmer's confusion when `x == z` returns `false` for two patrons with matching data.

Java's `equals()` method is the answer to both complaints: a separate, content-based criterion that must be explicitly defined. The company equivalent is a "same shipment" check — same contents, same origin, same destination — a business rule that exists alongside, not instead of, the identity-tracking system.

---

## What This Changes

The question that had no answer before: why did `patronA.age` change when the code only assigned to `patronC`? Without the reference model, this is an inexplicable mutation. The code appears not to touch `patronA`. The output contradicts the apparent logic. The bug has no location to investigate.

With the reference model, the same situation has a name — aliasing — and a specific cause: `patronC = patronA` copied an address, not an object. The mutation is not random. It follows directly from which address was stored in which variable at the moment of assignment.

Specific code and design decisions now look different. The `==` operator on objects is not broken — it is doing exactly what memory-address comparison requires. The `equals()` method is not redundant — it answers a different question about content. The constructor's role is clearer: it is the code that populates the heap block, not the code that creates the variable.

**Practice Bridge:** In the semester project, students create a domain class — a `Book`, a `Product`, an `Appointment`. The reference model applies directly: instantiate two objects, deliberately create a shared reference by assigning one variable to another, mutate through the alias, and observe the result. Annotate each line explaining what the stack holds and what the heap holds at that moment. This exercise makes the model testable before the first aliasing bug appears in project code.

The open question the model raises: if managing two patrons requires two named variables, how does a program manage a hundred patrons? The reference model is correct and complete for individual objects — but the manual variable-per-object approach does not scale. Arrays address this directly: an array is itself an object on the heap, reachable through a single reference, containing an ordered sequence of values or further references. That extension is the next application of everything above.

---

## Wonder Questions

1. If `patronC = patronA` copies the reference rather than the object, what would a genuine copy operation require? Which part of the program holds the information needed to duplicate field values — the reference variable, the heap block, or the class definition?

2. The `==` operator on reference types answers the identity question correctly for its intended use. What real-world question does identity comparison answer correctly that content comparison would answer incorrectly? When is it operationally necessary to know that two variables point to the same object, not merely equivalent objects?

3. A reference variable can hold `null`, meaning it stores no address and points to no object. When code tries to follow a null reference — `nullVar.age` — Java throws a `NullPointerException`. Using the reference model precisely, what is Java attempting to do at that instruction, and why does it fail?

4. Two patrons can legitimately share a library card in a real system — a family account. The current `Patron` class stores `libraryId` as a `String` field. What structural problem does this create when two `Patron` objects should reference the same account, and how does the reference model suggest modeling that relationship differently?

5. The chapter states that a class is a blueprint that exists before any instance is built from it. In terms of memory and execution, what is present when a class exists but no objects of that class have been created with `new`? What is absent from memory at that moment?

---

**Precision Summary**

**What the concept is:** The reference-versus-object model holds that a Java variable of object type stores a memory address — a reference — not the object's data. The object's data lives on the heap at that address.

**What it explains:** Aliasing — two variables pointing to one heap block, where a mutation through either name is visible through the other. Reference inequality — two variables built with identical arguments evaluating to `false` under `==` because they address two distinct heap blocks. Null pointer exceptions — a dereference attempt on a variable holding no address. The constructor's role — populating the heap block when `new` executes, not creating the variable.

**What it does NOT mean:** Java does not use references for everything. Primitive types (`int`, `double`, `boolean`) store values directly in the variable, not on the heap. The `==` operator is not defective — it compares addresses precisely as specified. The `equals()` method is not a correction to `==` — it answers a different question that programmers must define explicitly for each class.

**What comes next:** Arrays are heap objects reached through a single reference variable. A single array reference gives access to an ordered sequence of values or references. This is the mechanism by which one variable manages many objects — the direct extension of the model above, applied at the scale the project requires.
