<!--
    00-frontmatter.md
    FRONT MATTER — everything that appears before Chapter 1.

    Four sections in order:
      1. Title page
      2. Copyright page
      3. Dedication
      4. Preface

    The Preface is the authors' voice: why this book exists and why it
    matters now. The Introduction is the reader's roadmap.
-->

# INFO 5100 Application Engineering and Development

**Nik Bear Brown and Khaled Bugrara**

Northeastern University College of Engineering

First edition

---

## Copyright

Copyright © 2026 Nik Bear Brown and Khaled Bugrara. All rights reserved.

Published by Bear Brown, LLC.

No part of this publication may be reproduced, distributed, or transmitted in
any form or by any means without the prior written permission of the publisher,
except in the case of brief quotations in critical reviews and certain other
noncommercial uses permitted by copyright law.

ISBN: [INSERT ISBN]

First edition: 2026

---

## Dedication

For the students who learn programming not because syntax is beautiful by
itself, but because software gives them a way to build something useful in the
world.

---

## Preface

This book exists because introductory programming courses have acquired a new
problem. Students are still learning variables, loops, methods, objects,
inheritance, interfaces, collections, and graphical user interfaces. Those
topics have not disappeared. But students are now learning them in a world
where an AI assistant can produce plausible Java code before the student knows
enough Java to judge it.

That changes the work of teaching.

It is no longer enough to ask whether a student can make a program compile. It
is not even enough to ask whether the program appears to run correctly on a
simple example. The deeper question is whether the student can explain the
program's structure, trace its behavior, identify the responsibilities of its
objects, diagnose failures, and defend the design choices that connect code to
a real-world problem. If the answer is no, AI has not made the student more
capable. It has only made the gap harder to see.

INFO 5100 is an application engineering and development course. It introduces
Java and object-oriented design through the practical work of building GUI-based
applications. The course is not a language-reference tour. It is not a catalog
of every Java feature. It is an apprenticeship in turning a problem from the
world into a working software system: naming the objects, assigning
responsibility, representing state, responding to events, choosing data
structures, testing behavior, and explaining what the system does.

That apprenticeship matters more, not less, in the age of AI. The authors wrote
this book for learners who will almost certainly use AI tools while learning to
program. The right response is not to pretend those tools do not exist. The
right response is to teach students how to use them at the right moment, for the
right purpose, with the right verification discipline. AI can explain code,
suggest alternatives, generate scaffolding, and help debug. It cannot know the
student's actual requirement. It cannot take responsibility for the student's
design. It cannot appear at the final defense and explain why a class owns one
piece of behavior rather than another.

This book therefore treats Java, object-oriented design, GUI application
development, and AI collaboration as one learning problem. The student learns
to write Java, but also learns when generated code is useful, when it is
dangerous, and what evidence is required before accepting it. Each module
connects a programming topic to a professional habit: tracing, verification,
responsibility assignment, debugging by hypothesis, and explanation under
questioning.

Nik Bear Brown brings to the book a background in AI, machine learning,
software systems, data visualization, computational biology, and AI-native
learning infrastructure. Khaled Bugrara brings long experience in computer
science education, algorithms, information systems leadership, and applied
software projects that connect computing to real institutional needs. The book
is shaped by the shared conviction that programming education should not merely
produce code. It should produce engineers who can reason about code.

The reader should not expect perfection on the first pass. Programming is not
learned by reading alone. It is learned by making a prediction, running the
program, noticing the gap, and revising the mental model. That friction is not
an obstacle to learning. It is the mechanism of learning.

This book is for that friction.
