# Module 6 — Basics of GUI Programming in Java: Wonder Edition
## Companion Chapter
> **Wonder Edition:** Read this alongside the chapter, not instead of it.

---

## The Strange Question

Two login systems pass the demo. Both compile. Both reject wrong passwords. Both accept correct ones. A user runs them side by side and cannot tell them apart.

One of them has already failed its users.

The failure is not in the interface. It is not in the logic. The code works exactly as specified. Yet one of these systems, the moment its data file is read by the wrong person, hands every user's password to an attacker — including passwords those users use at their bank, their email, and their hospital.

What property must a correct login system have that is invisible to any user running it?

---

## First Intuition

Most programmers encountering authentication for the first time reason this way: the system accepts the right password and rejects the wrong one. That is the behavior. If the behavior is correct, the system is correct.

This intuition feels solid. A function that returns `true` for valid credentials and `false` for invalid ones has done its job. The user never sees what is stored. The attacker never runs the application. Why would storage format matter if the visible behavior is identical?

The intuition leads naturally to a design: store the username and password together. Read them at login. Compare. Done.

**Planning Metacognitive Prompt:** Before continuing, pause. Predict one scenario in which the application behaves perfectly for every legitimate user, yet causes real harm. Write the scenario in one sentence. Keep it. Come back to it after the next section.

---

## The Surprise

The scenario exists. It is not exotic. It is routine.

A developer commits a backup file to a public repository. A logging configuration writes too much to a monitoring dashboard. A server misconfiguration exposes a directory. A former employee retains read access to a file share longer than intended.

In each case, no one attacked the login screen. No one ran the application. No one tried a wrong password. They simply read a file.

But the file says `alice:password123`.

Alice used that password at four other sites. The attacker did not need to break anything. They needed only to read.

The system passed every behavioral test. It rejected wrong passwords. It accepted correct ones. It compiled cleanly. It worked. And yet it was already broken — not in what it did, but in what it stored.

**Monitoring Metacognitive Prompt:** Return to your predicted scenario. Did you anticipate a file read? If you predicted an attack on the running application, notice what your intuition defaulted to: runtime behavior. The chapter's central claim is about a different dimension entirely — a property the running application cannot demonstrate.

That property is still unresolved. A working login system stores something. What should it store?

---

## The Hidden Structure

The chapter introduces a one-way function called a hash. A hash takes any input and produces a fixed-length output. The same input always produces the same output. But given only the output, no efficient method recovers the input.

This single property changes what a file read exposes. A file containing `alice:ef92b778bafe771e89245b89ecbc08a44a4e166c` does not expose Alice's password. It exposes a value that was computed from her password but cannot be reversed into it. An attacker who reads this file cannot log in as Alice without computing the hash of every candidate password until one matches the stored value. That requires computational effort. Strong passwords make that effort impractical.

The design consequence is direct. The login system stores the hash, not the password. At login time, it hashes the supplied password and compares the result to the stored hash. The behavior is identical. The storage is fundamentally different.

**Misconception Checkpoint:** It is tempting to think that storing a hash is just another way of encoding the password — that the hash is the password in disguise. But encoding can be reversed; a hash cannot. The correct model holds that the hash is a one-way fingerprint: it proves that the right input was supplied without ever recording the input itself.

---

## Try Looking At It This Way

Consider a wax seal used on correspondence in the 17th century.

A sender melts wax onto a folded letter and presses a signet ring into it. The seal hardens. Anyone who receives the letter can see the impression and verify it matches the sender's ring. The impression proves the ring was present when the seal was made.

But the impression does not contain the ring. A forger who steals the sealed letter has the impression. They cannot reconstruct the ring from the wax. To create a new seal matching the original, they must obtain the ring itself.

Now map this to password hashing. The password is the signet ring — the secret. The hash is the wax impression — the record left behind. The login check is the verification step: does this impression match what this ring would produce? The credential file holds impressions. It does not hold rings.

The commonality is the one-way relationship: the ring produces the impression; the impression cannot reproduce the ring. The login system verifies by comparing impressions, not by recovering the original.

The mapping holds for the core security property.

---

## Where The Analogy Breaks

The wax seal analogy fails in one important way.

A wax impression is unique to a specific letter at a specific moment. Two letters sealed with the same ring look identical in impression. In password hashing, two users with the same password produce the same hash — a property called a collision on common inputs. Attackers exploit this by precomputing hashes of common passwords and scanning credential files for matches. This is a rainbow table attack.

The wax seal has no equivalent vulnerability because each seal is physically distinct. The hash does not share that property. Real systems address this with a random value called a salt, mixed into the hash computation, making each user's hash unique even if their passwords match. The chapter names this limitation explicitly. The analogy illuminates the one-way property. It does not capture the collision risk.

---

## Small Discovery

Consider a different domain: fingerprints.

Here is a data set. Four envelopes were sealed by hand. Three people touched envelope surfaces. Each person's finger left a pattern. The patterns were lifted and recorded:

- Envelope A: pattern 7734
- Envelope B: pattern 2291
- Envelope C: pattern 7734
- Envelope D: pattern 8815

A fourth envelope, sealed later, shows pattern 2291. A fifth shows pattern 9902.

**Pattern search:** Which envelopes were touched by the same person? How do you know?

**Guided prediction:** If investigators later find a suspect whose recorded fingerprint is pattern 7734, which envelopes can they connect to that suspect? Write your answer before continuing.

**Revelation:** Envelopes A and C connect to that suspect. The fourth envelope connects to whoever made pattern 2291 — that person touched two envelopes. Envelope D and envelope five connect to patterns that have not yet been matched to anyone.

Notice what just happened. The patterns identified people without containing any information about those people. A pattern is a one-way transformation of a physical surface. You can verify a match by comparing patterns. You cannot reconstruct the finger from the pattern.

The hash function does the same thing. It compares without containing. Verification does not require possession of the original.

---

## What This Changes

A reader who has worked through this chapter can now explain something that previously had no explanation: why two functionally identical systems are not equivalent.

The behavioral test — does the login accept correct passwords and reject wrong ones — evaluates one dimension. The storage test — if this file is read, what does the reader learn — evaluates a different dimension. The second dimension is invisible at runtime. It is visible only in the file.

This means testing a login system correctly requires asking a question that no automated test of normal operation will reveal. The reader can now formulate that question, apply it to any credential system, and evaluate the answer.

The question that comes next: what other properties of a system are invisible at runtime but critical for correctness? Session management — how the application knows a user is still authenticated after login — has this same character. Role enforcement — whether an authenticated user can only access resources they are permitted to see — has it too. The runtime behavior may look correct while the underlying model is broken. That pattern repeats across security-adjacent design problems.

---

## Wonder Questions

1. A system hashes passwords with SHA-256 and stores the hashes. An attacker obtains the file. The attacker also knows that most users of this application choose passwords under ten characters. Why does that second fact matter — and what does it reveal about the relationship between hash security and user behavior?

2. The chapter states that the `LoginManager.login()` method should return a boolean, not an enum distinguishing "username not found" from "wrong password." The enum would produce a better user experience. What property does the boolean protect that the enum would destroy — and why is that property invisible to a user testing the normal login flow?

3. A developer argues: "I will store passwords in Base64 encoding. It looks like a hash, the user cannot read it, and it requires no extra computation." Apply the threat-model question. What does an attacker gain if they read a file of Base64-encoded passwords? How does the answer differ from a file of SHA-256 hashes?

4. Every security recommendation in this chapter applies to the data-at-rest case: what an attacker learns from reading a stored file. What happens to these guarantees if the network connection between the login form and the server is unencrypted? Which part of the system does the hash protect, and which part does it leave unaddressed?

5. The chapter separates `Person` from `UserAccount` and argues that the `LoginManager` should not return the `Patron` object on login. This separation is presented as a security design. But it is also a design principle with a different name in object-oriented programming. What principle is it — and can a reader identify at least one other place in the chapter where the same principle appears under a different label?

---

**Precision Summary**

The core concept is the one-way hash as a storage strategy for credentials. It explains why two systems with identical runtime behavior can differ in their security properties — specifically, in what an attacker learns from reading stored data. It does not mean that hashing makes a system secure in all respects; it addresses only the data-at-rest exposure. It does not cover session management, authorization, network transmission, or the collision risk from unsalted common passwords. What comes next is the question of what authenticated users are permitted to do — the distinction between authentication and authorization that the chapter names but deliberately does not resolve.
