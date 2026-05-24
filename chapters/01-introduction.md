# Introduction

You cannot verify code you do not understand, and you cannot understand a system you only asked a machine to write.

That is the problem this book takes seriously. INFO 5100 is not a language-reference course, and it is not a prompt-engineering shortcut. It is a practicum in application engineering: building a complete object-oriented Java application while learning exactly where AI can help and exactly where the engineer must still understand, decide, debug, and verify.

The reader imagined here is a first-semester graduate student in an applied engineering or information systems program. They may have written Python or R scripts. They may have used Claude or another assistant to explain code. They have probably seen code that compiled before they understood why it worked. What they have not yet done is design, build, debug, test, and defend a complete Java application.

The book's central claim is plain: productive AI-assisted development requires real object-oriented understanding. AI can produce syntax, scaffolds, boilerplate, and candidate implementations. It cannot know whether a class boundary matches your business problem, whether a handler violates your model-view separation, whether a data-loss scenario matters to your users, or whether the final application satisfies the requirement you were actually given.

The course uses one threaded business problem across the semester. The text uses a library management system as the main example, while exercises invite inventory and healthcare scheduling variants. The point is compounding design: a class from Module 2 becomes part of a model in Module 5, a collection choice in Module 9, a GUI view in Module 10, and a defended design decision in Module 14.

## How This Book Is Organized

- **Module 0, Setup:** Install the JDK, NetBeans, and configure your first Java project without losing a lab session to tooling.
- **Module 1, Introduction: Socio-Technical Engineering and the Object Model:** Students learn why objects - not procedures - are the right mental model for business software, by running and breaking a working application before they write one.
- **Module 2, Creating and Displaying Multiple Objects:** Students learn to instantiate multiple objects from one class and trace how Java manages them in memory.
- **Module 3, User Interaction Design:** Students learn to design user flows as navigation between screens, connecting what the user sees to what the objects do.
- **Module 4, Finding Bugs: The Debugging Workflow:** Students learn a systematic debugging methodology - hypothesis, isolation, test - using the IDE debugger and their own reasoning, not error message reading alone.
- **Module 5, Modeling the Supply Side:** Students learn to model the entities that provide resources in a business system - the objects that exist before any user interacts with them.
- **Module 6, Designing the Person into the Application:** Students learn to model users and authentication as first-class objects - not as a database lookup, but as a designed part of the object system.
- **Module 7, Order Processing and Polymorphism:** Students learn why polymorphism is not a Java feature but a design strategy - the ability to add new types without changing existing code.
- **Module 8, Digital Ecosystems: Data Management and CRUD:** Students learn to design the full lifecycle of data in a business application - create, read, update, delete - and to implement it with file-based persistence.
- **Module 9, Targeting and Sorting: Working with Collections:** Students learn to sort, filter, and search collections of objects - and to choose the right collection type for each task.
- **Module 10, Introduction to GUI Programming with JavaFX:** Students learn to connect the object model they have built to a visual interface - understanding that the GUI is a view of the model, not the model itself.
- **Module 11, Event-Driven Programming: Making the Application Respond:** Students learn to connect user actions to application behavior using JavaFX event handling - and to maintain the model-view separation under the pressure of deadline.
- **Module 12, Advanced GUI: Scene Builder and Complex Interfaces:** Students learn to use Scene Builder to design complex interfaces while maintaining a clean boundary between the visual design and the application logic.
- **Module 13, Advanced Data: Collections, Unit Testing, and Lambda:** Students learn to write tests for their own code and use Java's advanced collection operations - and discover that untested code is code whose correctness you are guessing at.
- **Module 14, Final Project: Complete Application with Ecosystem Design:** Students complete, defend, and present a full GUI business application - and demonstrate, for every AI-assisted decision, what required their own engineering judgment.

## How To Read This Book

Read in sequence. The chapters are load-bearing. Skipping debugging makes later AI use unsafe. Skipping collections weakens GUI design. Skipping testing makes the final defense mostly theater.

Each module includes a HOW TO USE AI section. Treat those sections as part of the engineering content, not sidebars. The phase gates are the course's spine: AI may assist only when the student has enough understanding to verify what comes back.

The book excludes Spring, databases, Android, web development, deep concurrency, formal design-pattern coverage, and AI internals. Those are not unimportant. They are follow-on topics. This book builds the foundation needed to approach them without mistaking generated code for engineering judgment.
