# INFO 5100 Application Engineering and Development

**Authors:** Nik Bear Brown and Khaled Bugrara  
**Publisher:** Bear Brown, LLC  
**Copyright:** Copyright © 2026 Nik Bear Brown and Khaled Bugrara. All rights reserved.  
**Status:** Draft textbook for Kindle, online reading, and Medhavy integration

This book is an introduction to Java programming, object-oriented design, and
GUI-based application development for INFO 5100 Application Engineering and
Development. It teaches Java as an applied engineering practice: students learn
syntax and concepts, but also learn how to assign responsibility to objects,
trace program behavior, verify correctness, use AI tools responsibly, and
defend a real application.

The central claim is that AI-assisted programming makes object-oriented
understanding more important, not less. A student who cannot explain and verify
generated code cannot safely accept it. The book therefore pairs Java topics
with AI phase gates, verification habits, and project evidence.

## Table of Contents

| File | Title |
| --- | --- |
| `chapters/00-frontmatter.md` | Front Matter |
| `chapters/00-introduction.md` | Introduction |
| `chapters/00-welcome.md` | Module 0: Welcome |
| `chapters/01-fundamentals-of-programming-in-java.md` | Module 1: Fundamentals of Programming in Java |
| `chapters/02-methods-arrays-and-file-objects.md` | Module 2: Methods, Arrays, and File Objects |
| `chapters/03-objects-and-classes.md` | Module 3: Objects and Classes |
| `chapters/04-basics-of-object-oriented-programming-part-2.md` | Module 4: Basics of Object-Oriented Programming Part 2 |
| `chapters/05-inheritance-and-polymorphism.md` | Module 5: Inheritance and Polymorphism |
| `chapters/06-basics-of-gui-programming-in-java.md` | Module 6: Basics of GUI Programming in Java |
| `chapters/07-midterm-exam.md` | Module 7: Midterm Exam |
| `chapters/08-abstract-classes-and-interfaces.md` | Module 8: Abstract Classes and Interfaces |
| `chapters/09-event-driven-programming.md` | Module 9: Event-Driven Programming |
| `chapters/10-event-driven-programming-with-scene-builder.md` | Module 10: Event-Driven Programming with Scene Builder |
| `chapters/11-generics.md` | Module 11: Generics |
| `chapters/12-recursion.md` | Module 12: Recursion |
| `chapters/13-collections-and-iterators.md` | Module 13: Collections and Iterators |
| `chapters/14-lists-stacks-queues-and-the-final-project.md` | Module 14: Lists, Stacks, Queues, and the Final Project |
| `chapters/95-claude-code.md` | Appendix: Claude Code for Java |
| `chapters/97-fundamental-themes.md` | Appendix: Fundamental Themes |
| `chapters/99-back-matter.md` | Back Matter |

## Core Themes

- You cannot verify what you do not understand.
- Objects model responsibilities.
- Debugging is causal reasoning.
- AI use requires phase gates.
- The project is one system.
- Tests are evidence, not magic.
- The final defense demonstrates ownership.

## Medhavy Integration

This book is intended for Kindle, online reading, and Medhavy integration.
Medhavy, also written Medhavi, takes its name from मेधावी, meaning
"intelligent" or "intellectually brilliant." In Medhavy, the book can become an
intelligent textbook: searchable, adaptive, and connected to hints, examples,
practice, feedback, and review questions.

## Repository Structure

```text
book.md                 Book description and high-level planning notes
TIKTOC.md               Course and chapter planning document
chapters/               Markdown source chapters
images/                 Static SVG/PNG figures for EPUB and web output
d3/                     Interactive D3 figure implementations
pantry/                 Research and drafting notes
SCRIPTS/                Build and conversion utilities
output/                 Generated build output
```

## Build

```bash
npm install
./build.sh
```

SVG figures can be converted to PNG with:

```bash
node SCRIPTS/svg-to-png.mjs
```

## Rights

All rights reserved. See `LICENSE.md` for the full copyright and reuse notice.
