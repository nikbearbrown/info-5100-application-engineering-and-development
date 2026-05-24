# Introduction

The program runs. The button opens the window. The text field accepts input.
The list displays the books. A student clicks **Checkout**, sees no error, and
feels the small relief every new programmer recognizes: it worked.

Then the instructor asks a quiet question: where is the rule that prevents a
patron from checking out the same book twice?

The student scrolls. The rule might be in the button handler. It might be in
the `Book` class. It might be in the `Patron` class. It might be in a method an
AI assistant generated yesterday and the student has not fully read. The
application still runs, but the design has become hard to explain.

This book is about the gap between code that runs and software a student can
understand, verify, and defend.

The central argument is simple and contestable: in the age of AI-assisted
programming, object-oriented understanding is not less important. It is the
condition that makes AI assistance safe to use. A student who cannot explain
the responsibility of a class, trace a value through a method call, or test a
boundary case cannot responsibly accept generated code just because it compiles.
AI can accelerate implementation, but it cannot take ownership of the design.

This is that student's textbook.

It is written for learners in INFO 5100 Application Engineering and
Development: students who need to learn Java, object-oriented programming, GUI
application development, and disciplined AI use in the same semester. Some
readers will have written scripts before. Some will have used Python, R, or
JavaScript. Some will have copied code successfully without ever needing to
explain why it worked. The book begins where those learners actually are.

## What this book is

This book is an introduction to Java programming and object-oriented design
through the work of building GUI-based applications for real-world problems.
It teaches variables, data types, control flow, methods, arrays, file I/O,
classes, objects, constructors, inheritance, polymorphism, abstract classes,
interfaces, generics, recursion, collections, event-driven programming, and
JavaFX.

But the vocabulary of the book is not only Java vocabulary. It is also the
vocabulary of engineering judgment:

- What object owns this responsibility?
- What state must be true before this method runs?
- What evidence proves this behavior?
- What did AI generate, and what did the student verify?
- Where does a GUI event end and the model begin?
- What changes if the requirement changes?

The course description says students are expected to apply learned knowledge to
address an identified real-world problem. That sentence matters. A program is
not merely a collection of language features. It is a response to a problem.
The point of the Java is to make the response precise.

## What this book is not

This book is not a complete Java reference. It does not try to cover every API,
every language feature, or every professional framework. When you need exact
language rules, use the Java documentation. When you need exhaustive coverage,
use a reference text.

This book is also not an AI prompt cookbook. You will use AI, and the book will
tell you when and how, but the goal is not to outsource the work. The goal is
to become the kind of engineer who can use AI without being fooled by fluent
output.

Finally, this is not a course in software architecture at industrial scale. The
applications here are deliberately small enough to inspect. That is the point.
You cannot learn design responsibility from a system too large to hold in your
head. You learn it from a small system whose behavior you can trace, then carry
the habit forward.

## The themes underneath the modules

The appendix "Fundamental Themes" names the habits this book builds. They are
woven through the modules rather than saved for the end.

First: you cannot verify what you do not understand. This does not mean you
must know everything before using a library or tool. It means your
understanding must be sufficient for the behavior you are responsible for.
"AI wrote it" is not evidence. "It compiled" is not evidence. "It worked once"
is weak evidence. Verification requires a claim, a test, and an explanation.

Second: objects model responsibilities. A class is not a folder for related
functions. It is a decision about what a thing knows and what it is allowed to
do. A `Book` should not know about a button. A controller should not own a
business rule. A GUI should display state, not secretly become the model.

Third: debugging is causal reasoning. A debugger shows state; it does not
produce a theory. Real debugging begins when you can say, "I expect this
reference to point to this object at this moment, and if it does not, this is
the likely cause."

Fourth: AI use requires phase gates. The course changes what AI may do as your
verification ability grows. Early modules permit explanation and diagnosis.
Later modules permit scaffolding and candidate implementations. By the final
project, AI can be a collaborator, but the design judgment remains yours.

Fifth: the project is one system. A shortcut in Module 3 can become a bug in
Module 10. A clean boundary in Module 5 can make Module 14 easier to defend.
Design decisions compound.

Sixth: tests are evidence, not magic. A test tells you that a claim held for a
specific case. It does not prove all possible cases. Its value grows as the
project changes because it catches regressions that would otherwise remain
quiet.

Seventh: the final defense is the point. The running application matters, but
the defense reveals ownership. Can you explain why a class exists? Can you
trace a user action through the GUI into the model and back? Can you name what
AI helped with and what you checked yourself?

## The running thread

Many examples use a library checkout system because the domain is familiar.
Books, patrons, catalogs, loans, searches, checkouts, returns, files, lists,
buttons, and events are easy to picture. The domain is simple enough to learn
from but rich enough to expose real design questions.

You should not treat the library as the only possible application. The same
patterns apply to inventory systems, scheduling systems, patient transport
tools, student service platforms, and other real applications. The point is to
learn the shape of the responsibility, not memorize the library example.

## How the book is organized

**Module 0: Welcome** orients you to the course, the tools, academic integrity,
and the learning community.

**Module 1: Fundamentals of Programming in Java** reviews computation,
variables, data types, input/output, strings, control flow, loops, comments,
and basic design principles.

**Module 2: Methods, Arrays, and File Objects** introduces reusable behavior,
arrays, reading from files, writing to files, and manipulating file content.

**Module 3: Objects and Classes** turns from procedural programming to
object-oriented thinking: objects, classes, constructors, instance members,
static members, UML diagrams, and visibility.

**Module 4: Basics of Object-Oriented Programming Part 2** deepens object
thinking through object passing, arrays of objects, wrapper classes, strings,
`StringBuilder`, `StringBuffer`, and the `this` reference.

**Module 5: Inheritance and Polymorphism** introduces superclasses,
subclasses, constructor chaining, overriding, overloading, polymorphism,
dynamic binding, casting, `instanceof`, `equals`, protected members, and
`ArrayList`.

**Module 6: Basics of GUI Programming in Java** introduces GUI programming,
JavaFX, panes, controls, shapes, property binding, layout panes, polygons,
polylines, and Scene Builder.

**Module 7: Midterm Exam** checks cumulative programming proficiency,
including data structures, loops, conditionals, and problem-solving constructs.

**Module 8: Abstract Classes and Interfaces** teaches abstract methods,
abstract classes, interfaces, and classes that implement interface contracts.

**Module 9: Event-Driven Programming** introduces event sources, event
objects, handler classes, inner classes, `KeyEvent`, `KeyCode`, and the shift
from procedural execution to event response.

**Module 10: Event-Driven Programming with Scene Builder** extends JavaFX work
through Scene Builder, controller connections, event wiring, and more complex
GUI controls.

**Module 11: Generics** introduces generic classes, generic interfaces,
generic methods, wildcards, and the benefits of writing type-flexible code.

**Module 12: Recursion** teaches recursive methods through factorials,
Fibonacci, base cases, recursive cases, and the tradeoffs between recursive and
iterative solutions.

**Module 13: Collections and Iterators** introduces the Java Collections
Framework, the `Collection` interface, iterators, and the traversal of groups
of objects.

**Module 14: Lists, Stacks, Queues, and the Final Project** brings together
lists, comparators, queues, priority queues, stacks, and the final GUI
application project.

The appendices support the main sequence. The Claude Code appendix explains how
to use Claude Code responsibly for Java work. The Fundamental Themes appendix
collects the durable habits of mind that run through the course.

## How to read this book

Read the modules in order if you are taking the course. The sequence matters.
Later modules assume earlier design decisions, vocabulary, and habits. If you
skip, skip carefully: you can review a syntax topic out of order, but the
semester project is cumulative.

Each module gives you more than a concept. It gives you an action to perform,
an artifact to inspect, and an assessment that asks for evidence. Do not treat
the exercises as decoration. They are where the mental model gets built.

When the book asks you to predict before running code, actually predict. When
it asks you to trace, trace slowly. When it asks you to explain what AI did and
what you verified, write the explanation before polishing the code. The
artifact is not the only evidence of learning. The process matters.

## A note about AI

This book assumes AI is present. That is not a concession. It is the reality of
modern programming education and professional software work.

But the book makes a firm distinction between assistance and delegation. AI can
explain an error message. It can summarize a Java concept. It can draft a
method after you specify the requirement. It can suggest edge cases. It can
help refactor code. It can point out likely causes of a bug.

What it cannot do is be responsible for your program.

The reason is not mystical. It is practical. AI does not know what your
application is supposed to mean in its actual context. It can infer patterns
from text. It can produce code that resembles working code. But when the
requirement is ambiguous, when the domain has a hidden rule, when the GUI and
model disagree, when a test passes for the wrong reason, responsibility returns
to the engineer.

This is why the course uses AI phase gates. The boundary changes as your
ability changes. In early modules, you use AI mainly to explain and diagnose.
In later modules, you use it to generate candidate code, but only after you
have written the requirement and only before you verify the result. By the
final project, AI may be part of the workflow, but it is never the author of
your judgment.

If you remember only one sentence, remember this: AI can help you write code
faster than you understand it, and that is exactly why understanding matters.

## Tags

Java, object-oriented programming, software engineering, GUI programming,
JavaFX, event-driven programming, collections, recursion, generics, AI
assisted programming, Claude Code, application engineering, Northeastern
University, INFO 5100, Medhavy, intelligent textbook

The window opens. The button works. The program runs. Now explain it.

Let's go.
