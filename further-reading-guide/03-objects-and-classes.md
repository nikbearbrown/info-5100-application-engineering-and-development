# Module 3 — Objects and Classes: Further Reading

> **Content note:** Despite the title "Objects and Classes," this chapter focuses primarily on multi-screen GUI state management using Java Swing's `CardLayout`: how to pass object references between panels, enforce setter-before-show ordering, and assign ownership of mutable state across a navigation flow. The EDGE Learning Objectives (constructors, instance vs. static fields, accessor and mutator methods) appear as supporting material rather than as the chapter's primary argument. This guide addresses the actual chapter content — CardLayout navigation mechanics, reference identity, and separation of concerns — while also covering the class-design syntax the lab requires you to apply.

The chapter establishes that a user flow is a path through object state, not a sequence of screens, and it explains the two failure modes that follow from ignoring that distinction — lost reference and premature display. What it does not teach is the Java class anatomy required to build the objects that travel through that flow: how to declare private fields, write constructors that produce valid initial state, and define accessors that enforce the ownership rules the chapter describes only at the design level. Closing that gap is the first job of this guide. The second is providing the design vocabulary — separation of concerns as a principled engineering position, not just a course rule — so that you can evaluate design choices rather than memorize approved patterns.

Read the Key resource before your lab submission; it gives you the field, constructor, and method syntax the `Book` and `Loan` classes require. Choose one Recommended resource based on where the chapter left you least certain: use the Oracle static members tutorial if the instance-vs-static distinction felt abstract, and use the Bloch excerpt if you want to understand why the ownership rules are not arbitrary. The Further item is for students who want the theoretical foundation for separation of concerns; it is not required, assumes you can already write a complete Java class from scratch, and will take roughly 60–90 minutes.

---

### Key

**"Classes and Objects" — Oracle Java Tutorials (Lesson: Classes and Objects)**, Oracle Corporation, continuously updated (Java SE 21) | https://docs.oracle.com/javase/tutorial/java/javaOO/index.html

I included this because every setter method the chapter requires — `checkoutPanel.setBook(selectedBook)`, `confirmationPanel.setLoan(newLoan)` — depends on Java class syntax the chapter never demonstrates: private field declarations, constructors that set those fields to valid initial values, and public accessor and mutator methods that control external write access. Without this syntax, you can follow the chapter's logic but cannot implement the lab. Work through the "Declaring Classes," "Declaring Member Variables," "Providing Constructors for Your Classes," and "Returning a Value from a Method" subsections in order; each takes about 10 minutes. As you read, map each element directly to your flow table: every cell in the "fields read / fields written" columns names a field your domain class must declare. Skim the remaining subsections on `this` and nested classes for now.

> Supports: Graded Lab — Fundamentals of OOP. Before implementing the two-panel CardLayout flow with a traveling domain object, you need to construct the domain class (e.g., `Book`) with private fields and public accessors; the "Declaring Member Variables" and "Providing Constructors" subsections give you exactly that syntax.

---

### Recommended

**"Class Members" — Oracle Java Tutorials (Lesson: Classes and Objects, section: Understanding Class Members)**, Oracle Corporation, continuously updated (Java SE 21) | https://docs.oracle.com/javase/tutorial/java/javaOO/classvars.html

I included this because the chapter's EDGE objectives include static variables, constants, and methods, but the prose focuses entirely on instance state — and the distinction matters concretely for the lab. A static field belongs to the class, not to any instance, so every panel holding a `Book` reference shares the same static fields while having its own copy of instance fields. That asymmetry has a direct failure mode: if you accidentally declare a `selectedBook` field as `static` in a panel class, every navigation step overwrites a single shared reference, which appears correct until the flow is tested with a backward navigation or a second selection. Read this section in about 15 minutes, then audit each field declaration in your lab design and ask explicitly: should this belong to the class or to one instance? Freely available at the URL above; no institutional access required.

**_Effective Java_, Third Edition, Items 15–17** — Joshua Bloch, Addison-Wesley, 2018 | ISBN 978-0-13-468599-1 (available via institutional library or O'Reilly Learning)

Items 15–17 cover minimizing accessibility — why fields should be private and what a public field costs at scale. This is the resource that explains why the chapter's rule "decide which screen owns each field" is not an arbitrary course constraint but a standard industry practice with a documented failure mode when violated. Item 15 ("Minimize the accessibility of classes and members") is directly applicable to the `Book` and `Loan` classes the lab asks you to build: Bloch explains precisely what exposing a mutable field as `public` allows any caller to do to it, which is the design-level version of the chapter's warning about panels that write to fields they do not own. Read Items 15 and 17 closely; each is under eight pages. Item 16 can be skimmed.

---

### Further

**_Object-Oriented Analysis and Design with Applications_, Third Edition, Chapter 3 ("The Object Model")** — Grady Booch, Robert Maksimchuk, Michael Engle, Bobbi Young, Jim Conallen, and Kelli Houston, Addison-Wesley, 2007 | ISBN 978-0-201-89551-3 (available via institutional library)

This is a graduate-level software engineering text written for practitioners who design systems professionally, not a student tutorial; the prose assumes you are comfortable with class diagrams, encapsulation, and polymorphism and want to understand the theoretical principles that unify those concepts. The prerequisite before this resource rewards you is that you should be able to write a complete Java class — fields, constructor, accessors, mutators — without consulting syntax references, and you should have completed at least the lab's state-ownership table. Chapter 3 provides what the Recommended tier cannot: a systematic theoretical account of abstraction, encapsulation, modularity, and hierarchy as the four elements of the object model — which is the principled vocabulary behind the chapter's three-layer responsibility diagram (visibility to `CardLayout`, display to panels, state to domain objects). After reading it, you can articulate not just that mixing display logic and domain state is wrong, but which element of the object model the violation attacks and what the architectural consequence is. Expect 60–90 minutes; read Section 3.1 ("The Meaning of an Object") and Section 3.2 ("Relationships Among Objects") closely and use the rest for reference.
