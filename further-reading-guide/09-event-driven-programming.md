# Module 9 — Event-Driven Programming: Further Reading

This chapter introduces event handlers, event sources, and inner classes as they work in a JavaFX application — but it stops before explaining *why* the plumbing works the way it does. The resources below close two gaps: what actually happens when an event travels through the JavaFX scene graph before reaching your handler, and how the Observer pattern beneath every `EventHandler` connects this week's code to a broader design vocabulary you will use in every GUI project afterward. Closing those gaps now will make the handler-registration pattern feel inevitable rather than arbitrary, and will help you avoid the most common mistake — writing all logic inside the handler rather than delegating to the model.

Read the Key resource before the Optional Lab assessment. Choose one Recommended resource based on which concept felt least clear after the chapter: pick the JavaFX API entry if you are uncertain about `EventHandler` syntax, or the Oracle tutorial if you want to see handler patterns built up step by step. The Further item is for students who want to understand the design pattern underneath — it is not required and assumes comfort with interfaces and polymorphism beyond what this chapter teaches.

---

### Key

**JavaFX 21 API: Interface EventHandler\<T extends Event\>** — OpenJFX, 2023
*Scope: the `EventHandler` interface javadoc page at https://openjfx.io/javadoc/21/javafx.base/javafx/event/EventHandler.html, plus the linked `Event` and `EventType` pages (read all three together, approximately 20 minutes).*

I included this because the chapter registers handlers without explaining what `EventHandler<ActionEvent>` actually is — a functional interface with a single `handle(T event)` method — and that gap makes it hard to understand why a lambda expression is a legal handler. The API page shows the interface declaration, lists all event subclasses in the "See Also" section, and links to `EventType`, which explains how the type hierarchy works (why `KeyEvent.KEY_PRESSED` is a subtype of `KeyEvent.ANY`). Read the `EventHandler` page first, then follow the link to `EventType` and read the class description at the top. Stop there — the full method list is reference material, not required reading. This directly supports the learning objective of describing event sources and event classes: after reading it, you will be able to name what type each component in a handler registration plays.

---

### Recommended

**Handling JavaFX Events (Oracle Java Documentation)** — Oracle, 2023
*Scope: the "Event Processing Overview" and "Working with Event Handlers" sections of the JavaFX documentation trail at https://docs.oracle.com/javase/8/javafx/events-tutorial/events.htm (approximately 30 minutes; stop before the "Handling Mouse Events" subsection if time is short).*

I included this because the chapter shows handler registration but does not explain event routing — the fact that events travel *down* the scene graph (capture phase) and then *up* (bubbling phase) before reaching your handler. That routing is why `addEventFilter` and `addEventHandler` behave differently, and why consuming an event with `event.consume()` stops further propagation. The Oracle tutorial diagrams this clearly with a scene graph example. Read the "Event Processing Overview" section carefully and trace the diagram; then skim "Working with Event Handlers" to confirm the `addEventHandler` syntax matches what the chapter showed. This extends the chapter's apply-level objective: once you understand routing, you can explain *where* in the scene graph to place a handler for a given requirement.

**Using Inner Classes and Lambda Expressions as Event Handlers (Liang, *Introduction to Java Programming*, 11th edition, Chapter 15)** — Y. Daniel Liang, 2018
*Scope: Section 15.3 "Inner Classes" through Section 15.5 "Lambda Expressions," pages 582–601 (approximately 45 minutes).*

I included this because the chapter introduces inner classes as an event-handling technique but does not compare the three common forms — named inner class, anonymous inner class, and lambda expression — in a way that lets you choose deliberately among them. Liang's Chapter 15 is structured as a progression: it shows the verbose named-inner-class handler first, then collapses it to anonymous, then to lambda, making the equivalence explicit. Read sequentially; the "why" of each collapse is in the paragraph between each code sample, and skipping those paragraphs defeats the purpose. This supports the chapter's learning objective on handler classes: you will leave able to write the same handler three ways and explain the tradeoff (readability vs. reusability).

---

### Further

**"Observer" in *Design Patterns: Elements of Reusable Object-Oriented Software*** — Gamma, Helm, Johnson, Vlissides (Gang of Four), 1994
*Scope: Chapter 5, the Observer pattern entry, pages 293–303 (approximately 60–90 minutes; the Motivation and Applicability sections are the payoff; the Implementation section is optional for this course).*

*Level note: This is a classic software-engineering text written for professional programmers; the prose assumes fluency with polymorphism, interfaces, and object composition beyond what this chapter requires. It is not difficult prose, but it will feel abstract if interfaces still feel shaky.*

*Prerequisite: You should be comfortable with the idea that an interface defines a contract and that multiple classes can implement the same interface. If the `EventHandler<ActionEvent>` syntax in this chapter still feels foreign, read the Key resource first and return to this one when handler registration feels routine.*

*Payoff: The Recommended tier explains how JavaFX event routing works mechanically. This entry explains *why* the Observer pattern was invented — the problem it solves, the coupling it avoids, and the tradeoff it introduces (subjects do not know what their observers will do, which is power and risk simultaneously). After reading it, JavaFX `EventHandler` registration will stop looking like JavaFX syntax and start looking like a named design pattern you will recognize in every event-driven framework you encounter professionally — Android listeners, JavaScript DOM events, Python Tkinter callbacks. That portability is what the Recommended tier cannot give you.*

---

> **Assessment connection:** The Key resource (the `EventHandler` interface javadoc) directly supports the Optional Exercise "Creating a JavaFX application with a response for user action." Before writing the handler registration, read the `EventHandler<T>` interface declaration and confirm which type parameter `T` should be for a button-click handler versus a key-press handler — that decision is what the exercise is testing.
