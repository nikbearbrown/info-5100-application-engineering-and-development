# Module 5 — Inheritance and Polymorphism: Wonder Edition
## Companion Chapter

> **Wonder Edition:** Read this alongside the chapter, not instead of it.

---

## The Strange Question

A variable is declared as type `Animal`. The object it points to is a `Dog`. The program calls `makeSound()` on the variable. Java runs the `Dog` version of the method — not the `Animal` version.

The variable never knew it held a `Dog`. The compiler only saw `Animal`. No one checked which class the object belonged to at runtime.

How did Java know which method to run?

---

## First Intuition

Most people reach for the same answer: Java looked at the variable's declared type and picked the matching method.

That is what seems to happen. The variable is `Animal`. The method exists on `Animal`. Java runs it. Simple.

The declared type is a contract — it tells the compiler what operations are legal. If `Animal` has `makeSound()`, then calling `makeSound()` on any `Animal` variable is legal. No surprise there.

What the declared type does *not* seem to do is pick which version runs. That feels like it should also depend on the declared type. If the variable says `Animal`, the `Animal` method should run. Why would Java look further?

> **Planning Metacognitive Prompt:** Before reading on, write one sentence predicting what information Java actually uses to pick the method version at runtime. Be specific about when that decision happens — at compile time or at runtime — and why.

---

## The Surprise

Here is the contradiction that breaks the intuition.

Write two classes: `Animal` with a `makeSound()` method that prints "generic sound," and `Dog` that extends `Animal` and overrides `makeSound()` to print "bark." Declare a variable `Animal a = new Dog()`. Call `a.makeSound()`.

The compiler sees `Animal`. It allows the call. It does not complain.

But the program prints "bark."

The `Animal` version of `makeSound()` was never called. The variable said `Animal`. The compiler agreed it was `Animal`. At no point did anyone write `Dog` where the method was called.

And yet: "bark."

The declared type did not pick the method. Something else did. The compiler did not decide. Something later decided.

> **Monitoring Metacognitive Prompt:** Does this surprise you, or did you predict it? If you predicted it, name the mechanism you expected. If it surprises you, name the assumption that is now broken. Hold that broken assumption in mind — the next section will need it.

The question sits open: if not the declared type, what decided? And when?

---

## The Hidden Structure

The declared type determines what method *names* are legal to call. The actual object's class determines *which version* of that method runs.

These are two separate decisions, made at two separate times. The compiler handles the first at compile time — it checks that `makeSound()` exists on `Animal`. The JVM handles the second at runtime — it looks at the actual object sitting in memory, finds its class, and runs that class's version of the method.

This is dynamic binding. The binding between the method call and the method body happens dynamically, at runtime, based on the object's actual type.

> **Misconception Checkpoint:** It is tempting to think that the declared type of a variable determines which method version runs. But the declared type only determines which method names are *accessible*. The correct model holds that the JVM dispatches method calls based on the runtime type of the object — the class used in the `new` expression — not the type of the reference variable.

The concept has a name: polymorphism. A single method call behaves differently depending on which object receives it. The word means "many forms." One call site, many possible behaviors, resolved at runtime.

Inheritance is what makes polymorphism possible. A subclass inherits the method signature from its superclass. It can override the body. The reference variable can hold any object in the inheritance hierarchy. The JVM looks at the actual object and dispatches accordingly.

Without inheritance, no shared signature exists. Without a shared signature, the compiler cannot accept the call through a superclass reference. Without dynamic binding, the runtime would not know to look at the actual object. The three mechanisms — inheritance, overriding, dynamic binding — are not three separate ideas. They are three parts of one mechanism.

---

## Try Looking At It This Way

**The analogy: a theater with an understudy.**

Consider a Broadway play. The playbill lists a role: "Hamlet." The theater sells tickets to see Hamlet. Every ticket buyer knows Hamlet will appear. The contract is clear.

Now consider two actors who can play Hamlet: the lead and the understudy. Both know the lines. Both can perform the role. From the audience's perspective, the character is Hamlet either way.

The theater is the declared type — it guarantees Hamlet appears. The actor who walks on stage is the actual object. The audience calls out "Hamlet" — one call, one name. The actor who responds is determined at showtime, not when the tickets were printed.

**The base domain:** A theater role is a contract. Multiple actors can fulfill it. The audience interacts with the role, not the specific actor.

**The target domain:** A superclass reference is a contract. Multiple subclass objects can fulfill it. Code interacts with the superclass interface, not the specific subclass.

**Mapping the features:**
- Theater role → declared superclass type
- Specific actor → actual subclass object
- Audience calling for Hamlet → code calling a method on a superclass reference
- Actor who responds → JVM dispatching to the subclass's method version
- Showtime decision → runtime dispatch (dynamic binding)

**What the analogy explains:** The audience does not need to know which actor is performing. Code does not need to know which subclass is instantiated. Both rely on the contract — the role, the declared type — and trust the runtime to deliver the right performer.

**What the analogy does not explain:** See the next section.

---

## Where The Analogy Breaks

An actor decides whether to go on stage. A `Dog` object does not decide anything. Dynamic binding is mechanical, not intentional.

More importantly: the theater analogy implies two actors compete to play the same role. In Java, a subclass does not compete with its superclass. The subclass *replaces* the superclass method for objects of its type. There is no negotiation. There is no fallback to the superclass version unless the subclass explicitly calls `super.makeSound()`.

The analogy also misses casting. Code can ask at runtime whether an `Animal` reference actually holds a `Dog` — using `instanceof` — and then cast to `Dog` to call `Dog`-specific methods that are not on `Animal`. No theater analogy captures this. When the audience calls for Hamlet, they cannot also call for understudy-specific behavior the role does not define.

Use the theater analogy to understand why a single call site can trigger different behaviors. Do not use it to reason about casting, `instanceof`, or `super`.

---

## Small Discovery

Here is a small inquiry in a different domain. Work through each step before reading the next.

**The raw data:** A hospital employs nurses, doctors, and administrators. All three groups clock in and out. The hospital's time-tracking system records one event per person per shift: a clock-in timestamp and a clock-out timestamp. The system was built ten years ago, before the hospital expanded.

Suppose the hospital now wants to add a new kind of staff member: a traveling surgeon who works irregular schedules and bills by procedure, not by hours. The surgeon needs to clock in and out like everyone else, but also needs to log each procedure separately.

**Pattern search:** The existing system tracks one thing for all staff: time. The new staff member needs to track two things: time and procedures. What does the existing system need to know about the new staff member type? What does it not need to know?

**Guided prediction:** Before reading on — predict: can the hospital add the new surgeon type to the existing time-tracking system without rewriting the clock-in and clock-out logic? What would make that possible? What would make it impossible?

Write your prediction. Be specific.

**The revelation:** The hospital can add the surgeon type to the time-tracking system without touching the clock-in and clock-out logic — if and only if the surgeon class inherits from the same base class (or implements the same interface) that all other staff types use. The existing system calls `clockIn()` and `clockOut()` on staff objects through a shared reference type. If `TravelingSurgeon` extends `StaffMember` and overrides nothing about clock-in behavior, the time-tracking system calls its `clockIn()` exactly as it calls everyone else's.

The procedure logging is new behavior. It exists on `TravelingSurgeon` alone. The time-tracking system never calls it — it only calls the inherited methods. Code elsewhere in the hospital system, which *knows* it has a `TravelingSurgeon`, can call the procedure-logging methods directly.

The discovery: inheritance lets a system grow without touching the code that already works. The existing time-tracking logic is closed for modification. The surgeon type is open for extension. This is not a coincidence — it is why the mechanism exists.

---

## What This Changes

A reader who has worked through this section can now explain three things that were previously invisible.

First: why a method call on a superclass reference runs the subclass method. The declared type governs which calls are legal. The actual object's class governs which body runs. These decisions happen at different times.

Second: why adding a new subclass does not require rewriting the code that uses the superclass reference. The existing code makes no assumptions about which specific subclass is present. It only assumes the contract defined by the superclass is fulfilled.

Third: why polymorphism is not just a naming convention or a style preference. It is the mechanism that lets one piece of code work correctly with objects it has never seen, provided those objects fulfill a known contract.

The question that opens next: if code can hold any subclass in a superclass reference, how does code safely access behavior that only exists on one specific subclass? That is the question `instanceof` and casting answer — and they carry risks that the module's next layer addresses.

---

## Wonder Questions

1. The JVM uses the actual runtime type to dispatch a method call. But the compiler uses the declared type to check whether the call is legal. What happens when a subclass defines a method that does not exist on the superclass — can a superclass reference ever reach it? Why or why not?

2. Two classes both define `makeSound()`, but neither inherits from the other. A method takes an `Object` parameter — the root of all Java classes — and calls `makeSound()` on it. What happens? What does this reveal about what polymorphism actually requires?

3. A subclass overrides a method from its superclass. Inside the override, it calls `super.makeSound()`. The superclass version runs first, then the subclass adds its own behavior. Who decides the order? Is there a case where this order is wrong?

4. The hospital's time-tracking system works without knowing about `TravelingSurgeon`. But if the hospital adds one hundred new staff types over ten years, and some of them override `clockIn()` in subtle ways, how does a maintainer know which version of `clockIn()` actually runs for a given staff member? Is that a problem with polymorphism, or a problem with something else?

5. Java allows a variable declared as `Object` to hold any Java object. Every class inherits from `Object`. Does this mean every Java program already uses polymorphism, even if no one wrote a subclass? What is missing from that claim?

---

> **Precision Summary**
>
> **What this concept is:** Dynamic binding is the mechanism by which Java selects a method body at runtime based on the actual type of the object, not the declared type of the reference variable.
>
> **What it explains:** How a single method call on a superclass reference can produce different behavior depending on which subclass object is present — without any conditional logic at the call site.
>
> **What it does NOT mean:** It does not mean the declared type is irrelevant. The declared type determines which method names are legal to call. Dynamic binding only operates within that boundary.
>
> **What comes next:** When code needs behavior that exists only on a specific subclass — not on the declared superclass type — it must check the object's runtime type explicitly, using `instanceof`, and cast before calling. That is where the mechanism gains power and gains risk in equal measure.
