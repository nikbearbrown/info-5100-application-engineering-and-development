# Module 6 — Basics of GUI Programming in Java: Wonder Edition
## Companion Chapter
> **Wonder Edition:** Read this alongside the chapter, not instead of it.

> **Content note:** Despite the title "Basics of GUI Programming in Java," this chapter covers authentication design, password hashing, credential storage, and threat modeling. This companion follows the actual chapter content.

---

## The Strange Question

Two login systems pass the demo. Both compile. Both reject wrong passwords. Both accept correct ones. A user runs them side by side and cannot tell them apart.

One of them has already failed its users.

The failure is not in the interface. It is not in the logic. The code works exactly as specified. Yet one system, the moment its data file is read by the wrong person, hands every user's password to an attacker — including passwords those users use at their bank, their email, and their hospital portal.

What property must a correct login system have that is invisible to every user running it?

---

## First Intuition

Most programmers encountering authentication for the first time reason from behavior. The system accepts the right password and rejects the wrong one. That is the behavior. If the behavior is correct, the system is correct.

This intuition feels solid. A function that returns `true` for valid credentials and `false` for invalid ones has done its job. The user never sees what is stored. The attacker never runs the application.

The intuition leads naturally to a design: store the username and password together. Read them at login. Compare. Done.

This intuition comes from a reasonable place. Most software errors show up in running programs. A developer who has spent years chasing bugs learns to trust the test that passes. Password storage breaks a different rule — one that only activates when the data leaves the system.

> **► Planning prompt:** Write down the model you are using right now. What experience taught you to trust behavioral tests? What are you predicting the chapter will argue is wrong about that trust? Write it before continuing.

---

## The Surprise

The scenario exists. It is not exotic. It is routine.

A developer commits a backup file to a public repository. A logging configuration writes too much to a monitoring dashboard. A server misconfiguration exposes a directory listing. A former employee retains read access to a file share longer than intended.

In each case, no one attacked the login screen. No one ran the application. No one tried a wrong password. They simply read a file.

But the file says `alice:password123`.

Alice used that password at four other sites. The attacker did not need to break anything. They needed only to read.

The system passed every behavioral test. It rejected wrong passwords. It accepted correct ones. It compiled cleanly. It worked. And yet it was already broken — not in what it did, but in what it stored.

> **► Monitoring prompt:** What assumption did your intuition rely on — that attacks come through the application's running interface? What concrete scenario just contradicted that? What remains unexplained: why does the login still work correctly even after changing what is stored?

---

## The Hidden Structure

Therefore, a correct login system must be evaluated on two dimensions, not one. The first is behavioral: does it accept valid credentials and reject invalid ones? The second is storage: if this file is read, what does the reader learn?

The chapter introduces a one-way function called a hash. A hash takes any input and produces a fixed-length output. The same input always produces the same output. Given only the output, no efficient method recovers the input. This single property changes what a file read exposes.

A file containing `alice:ef92b778bafe771e89245b89ecbc08a44a4e166c` does not expose Alice's password. It exposes a value computed from her password that cannot be reversed. An attacker who reads this file cannot log in as Alice without computing the hash of every candidate password until one matches. That requires effort. Strong passwords make it impractical.

**Misconception Checkpoint:**

> "It is tempting to think that storing a hash is just another way of encoding the password — that the hash is the password in disguise, like Base64 or a Caesar cipher. But encoding reverses; a hash does not. The correct model holds that the hash is a one-way fingerprint: it proves that the right input was supplied without ever recording the input itself. The key distinction is the direction of computation: encoding is a two-way transform, hashing is a one-way trap door."

**Code Trace — Hash Storage vs. Plaintext Storage:**

```java
// BROKEN: stores the raw password
public UserAccount(String username, String password, String patronId) {
    this.username = username;
    this.passwordHash = password;       // plaintext — file read exposes everything
    this.patronId = patronId;
}

// CORRECT: stores the hash of the password
public UserAccount(String username, String password, String patronId)
        throws Exception {
    this.username = username;
    this.passwordHash = hash(password); // one-way — file read exposes only the hash
    this.patronId = patronId;
}

public boolean checkPassword(String supplied) throws Exception {
    return hash(supplied).equals(this.passwordHash); // compare hash to hash
}
```

The broken version stores `password` directly. The correct version calls `hash(password)` at storage time and calls `hash(supplied)` again at verification time. The running behavior is identical. The file contents are not.

---

## Try Looking At It This Way

**Target:** Password hashing in a login system

**Base:** A wax seal pressed by a signet ring onto a folded letter in 17th-century correspondence

**Features:**
- The ring produces an impression in the wax. The same ring always produces the same impression shape.
- Anyone receiving the letter can compare the wax impression to a known impression from the same ring to verify authenticity.
- The impression is permanent and stable — it does not degrade into the ring that made it.

**Commonalities (WHY each):**
- *Same input, same output:* The same ring always produces the same impression, just as the same password always produces the same hash. Both systems rely on deterministic reproduction for verification.
- *One-way relationship:* A forger who steals a sealed letter has the impression. They cannot reconstruct the ring from the wax alone. The hash file holder has the hash. They cannot reconstruct the password from it.
- *Verification without possession:* The recipient verifies the seal by comparing impressions, not by recovering the ring. The login check verifies credentials by comparing hashes, not by recovering the password.

**Boundaries:**
- The analogy describes the one-way verification property. It does not cover what happens when two users choose the same password — both produce the same hash, a collision risk that wax seals do not share because each physical seal is slightly unique. Real systems address this with a random salt mixed into the hash computation.

**Conclusions:**
The wax seal clarifies why the login system can verify without storing. The receiver does not need the ring to check authenticity. The server does not need the password to check credentials. The file holds impressions. It does not hold rings.

---

## Where The Analogy Breaks

Unlike the wax seal, the hash function does not produce a physically unique impression for each use. Two users with identical passwords produce identical hashes. Attackers exploit this by precomputing hashes of common passwords — "password123," "letmein," "qwerty" — and scanning a credential file for matches. This is a rainbow table attack. The wax seal has no equivalent vulnerability because physical seals vary slightly with each impression. This matters because a credential file full of SHA-256 hashes without salting is vulnerable to this precomputed lookup in ways that the analogy does not predict. The chapter names this limitation and points to bcrypt and Argon2 as the production-level solution.

---

## Small Discovery

Consider a different domain entirely: forensic serology in criminal casework.

Here is the raw data. A laboratory receives five blood samples from a crime scene investigation. Each sample is typed using ABO blood group analysis — a standard forensic procedure since the 1920s. The results:

- Sample A: Type O
- Sample B: Type A
- Sample C: Type O
- Sample D: Type B
- Sample E: Type A

A suspect is typed and found to be Type O.

**Pattern search:** Which samples could have come from the suspect? Which cannot?

**Prediction:** Before reading further, write down which samples are consistent with the suspect, which are excluded, and what you cannot determine from this data alone.

---

Samples A and C are consistent with the suspect. Samples B, D, and E are excluded — the suspect's blood type cannot produce those markers. But consistency is not identity. Type O is the most common blood type worldwide. The match rules out some people. It does not identify a single individual.

**Revelation — Verification Without Recovery:** Blood typing proves that the right type was present without identifying the person. Hashing proves that the right password was supplied without recording the password. Both systems compare a property of the original rather than the original itself. Both can exclude non-matches definitively. Neither can recover the source from the property alone. The forensic implication: a match is necessary but not sufficient evidence. The authentication implication: a hash match is necessary and sufficient for login — but the hash cannot be reversed to recover the password if lost.

---

## What This Changes

A reader who has worked through this chapter can now answer a question that previously had no answer: why two systems with identical runtime behavior are not equivalent. The behavioral test evaluates one dimension. The storage test evaluates a different dimension. The second dimension is invisible at runtime.

Specific code design looks different after this chapter. A `UserAccount` constructor that accepts a password string and stores it directly is now visibly wrong — not because it fails tests, but because it fails the storage-dimension question. A login method that returns an enum distinguishing "username not found" from "wrong password" is now visibly problematic — not because the UI breaks, but because the distinction helps attackers enumerate valid usernames.

> **► Practice Bridge:** Implement `LoginManager.login()` so that it hashes the supplied password using `MessageDigest` SHA-256 before comparing it to the stored hash in `UserAccount`. Verify two things manually: (1) a correct password passes after hashing in both directions, and (2) the method returns the same `false` response whether the username is absent or the password is wrong — giving the caller no information about which failure occurred.

The open question this chapter leaves is authorization. Users can log in. What can different user types do after login? That question requires a different design mechanism — role enforcement — and a different threat-model row: not "what does file read expose?" but "what can an authenticated user access that they should not?"

---

## Wonder Questions

1. A system hashes passwords with SHA-256 and stores the hashes. An attacker obtains the credential file and also knows that most users of this application choose passwords under ten characters. Why does that second fact matter — and what does it reveal about the relationship between hash security and user behavior?

2. The chapter states that `LoginManager.login()` should return a boolean, not an enum distinguishing "username not found" from "wrong password." The enum would improve the user experience. What property does the boolean protect that the enum destroys — and why is that property invisible to a user testing normal login behavior?

3. A developer argues: "I will store passwords in Base64 encoding. It looks like a hash, the user cannot read it directly, and it requires less computation." Apply the threat-model question. What does an attacker gain when they read a file of Base64-encoded passwords? How does that answer differ from a file of SHA-256 hashes?

4. The chapter separates `Person` from `UserAccount` and argues that `LoginManager` must not return the `Patron` object on successful login. What coupling does that separation prevent — and which downstream problem does the `patronId` string (instead of a `Patron` reference) specifically avoid when new features require iterating over all patrons?

5. Every security property discussed in this chapter applies to data at rest: what an attacker learns from reading a stored file. What happens to these guarantees if the network connection between the login form and the application is unencrypted? Which part of the system does SHA-256 hashing protect, and which part does it leave entirely unaddressed?

---

**Precision Summary**

**What the concept is:** A one-way hash function as the storage strategy for credentials — computing a fixed-length fingerprint from a password that verifies the original input without recording it.

**What it explains:** Why two login systems with identical runtime behavior differ in their security properties — specifically, what an attacker learns when they read the credential file rather than attack the running application.

**What it does NOT mean:** Hashing makes a system fully secure. SHA-256 without salting remains vulnerable to rainbow table attacks on common passwords. Hashing addresses data-at-rest exposure only. It does not address network transmission, session management, authorization, or the collision risk from unsalted identical passwords.

**What comes next:** Authorization — determining what authenticated users are permitted to do. That question requires role enforcement, a different design mechanism, and its own threat-model row. The chapter names it deliberately without resolving it.
