# Worked Exercises: Basics of GUI Programming in Java

*Chapter 6 of INFO 5100 Application Engineering and Development*

> These exercises follow a research-backed sequence: full worked example → matched practice → completion problem → error-recognition → transfer → interleaved review. Each section builds on the previous. Do not skip ahead.

---

## Prerequisites

- You can write a Java class with private fields and a constructor, and you can use a `HashMap<String, V>` with `put` and `get`.
- You understand the chapter's core distinction: a **Person** (the domain participant — `Patron`, `Employee`, `Patient`) is separate from a **UserAccount** (the credential), which links to the person *by ID, not by reference*.
- You can articulate what a **hash** is — the fixed-length, deterministic, one-way output of a function — and what a **threat model** answers: "if someone reads my user database, what can they do?"

---

## Part A — Full Worked Example

**What this demonstrates:** Separating the credential from the person, storing a SHA-256 **hash** instead of a plaintext password, and writing a **LoginManager** that answers only "are these credentials valid?" — verified against a written **threat model**.

**The problem:** A login system stores credentials like `alice:password123` and checks login by comparing the stored field to the supplied password with `.equals()`. The demo passes — correct credentials are accepted, wrong ones rejected — but if anyone reads the credential file, every user's password is exposed. Build the separated, hashed design instead.

**The solution:**

**Step 1 — Answer the threat-model question in writing, before any code.** Fill the table for the library domain:

| Threat | Plaintext system | Hashed system |
| --- | --- | --- |
| File read | All passwords exposed immediately | Dictionary attack required; strong passwords safe |
| Application compromise | Attacker logs in as any user | Same as file read |
| Credential reuse | Other accounts (email, banking) at risk | Damage limited to weak passwords |

*Why:* The **threat model** converts "security is important" into a specific question with a specific answer. The table is the spec; the code implements the table.
*Check:* For the row "File read," the hashed system's answer is "dictionary attack required" — that is the property the implementation must achieve.

**Step 2 — Model the Person separately from the credential.** `Patron` holds only business data and knows nothing about passwords.

```java
public class Patron {
    private String patronId;
    private String name;
    // constructor, getters, domain methods — NO passwordHash field
}
```

*Why:* A **Person** record exists because the business needs it; a credential exists because the system needs to control access. Mixing them puts authentication data on every object that handles `Patron`.
*Check:* `Patron` has no `passwordHash` and no login logic. The security surface does not touch it.

**Step 3 — Hash the password inside UserAccount, linking by ID.** `UserAccount` stores the username, the hash, and the patron *id string*.

```java
public class UserAccount {
    private String username;
    private String passwordHash;
    private String patronId;          // links to Patron by ID, not by reference

    public UserAccount(String username, String password, String patronId) throws Exception {
        this.username = username;
        this.passwordHash = hash(password);   // hash on storage
        this.patronId = patronId;
    }
    public String getUsername() { return username; }
    public boolean checkPassword(String supplied) throws Exception {
        return hash(supplied).equals(this.passwordHash);   // hash on verification
    }
}
```

with the chapter's `hash` method:

```java
public static String hash(String password) throws Exception {
    MessageDigest digest = MessageDigest.getInstance("SHA-256");
    byte[] encoded = digest.digest(password.getBytes(StandardCharsets.UTF_8));
    StringBuilder hex = new StringBuilder();
    for (byte b : encoded) hex.append(String.format("%02x", b));
    return hex.toString();
}
```

*Why:* Storing `patronId` (a key) rather than a `Patron` reference keeps the credential object from carrying the patron's borrowing history. The same `hash` runs on storage and on verification so the comparison is valid.
*Check:* `UserAccount` holds a `String patronId`, not a `Patron`. The hash is computed in both directions with the identical algorithm.

**Step 4 — Write LoginManager over a HashMap; return a boolean.**

```java
public class LoginManager {
    private Map<String, UserAccount> accounts = new HashMap<>();
    public void addAccount(UserAccount account) {
        accounts.put(account.getUsername(), account);
    }
    public boolean login(String username, String password) throws Exception {
        UserAccount account = accounts.get(username);
        if (account == null) return false;
        return account.checkPassword(password);
    }
}
```

*Why:* The **HashMap** keyed by username gives O(1) average-case lookup — the only query this component needs. `login` answers one question (valid or not); it does not return the `UserAccount` or the `Patron`.
*Check:* Trace the login flow:

| Step | Call | Result |
| --- | --- | --- |
| 1 | `login("alice", "library2024")` | enters method |
| 2 | `accounts.get("alice")` | returns the `UserAccount` (non-null) |
| 3 | `account.checkPassword("library2024")` | `hash("library2024").equals(storedHash)` |
| 4 | hashes match | returns `true` |
| 5 | wrong password `"guess"` | `hash("guess")` ≠ storedHash → `false` |

**Step 5 — Verify the separation by tracing what login does NOT touch.** Confirm: authentication never retrieves the `Patron` object; `login` returns a boolean, not a person; a failed login does not reveal whether the username or the password was wrong.
*Why:* The separation *is* the design and the verification target. Returning the same `false` for "username not found" and "wrong password" prevents an attacker from enumerating valid usernames.
*Check:* If authentication succeeds and the app needs Alice's record, a *separate* lookup uses `patronId` — authentication and domain-data access are distinct operations.

**Final answer:** Three separated objects — `Patron` (Person), `UserAccount` (credential, linked by `patronId`, password SHA-256 hashed), `LoginManager` (HashMap directory, returns boolean). The threat-model table is written first and the code implements it.

**What made this work:** The central concept is **separating the person from the account** and **hashing the credential** so the threat-model answer to "if someone reads my user database, what can they do?" is bounded by password strength rather than "everything." The naive approach — storing plaintext and comparing with `.equals()` — passes the demo identically but fails the threat model: one file read hands over every password, and because people reuse passwords, the damage extends to accounts that have nothing to do with this application.

**Self-explanation prompt:** In your own words, why does storing `patronId` as a String instead of a `Patron` reference protect the separation of concerns, even though a reference would be more convenient?

---

## Part B — Matched Practice Problem

**The problem:** Build authentication for an inventory system. The domain participant is `Employee` (employeeId, name — used to audit which employee made which stock adjustment). Build: (1) the **threat model** table for the inventory domain, written first; (2) `Employee` with no credential field; (3) `UserAccount` storing username, SHA-256 `passwordHash`, and `employeeId` *by ID, not reference*, with `checkPassword`; (4) `LoginManager` over a `HashMap<String, UserAccount>` whose `login` returns a boolean; (5) a trace table of a successful and a failed login.

Produce all five. The `LoginManager.login` must not return the `Employee` object, and the hash must be computed on both storage and verification.

**Stuck?** Ask the threat-model question for *this* domain first: if someone reads the inventory credential file, what can they do — and does the answer differ from the library because of what the stolen credentials unlock?

*Instructor note: No solution is provided for Part B. Write the threat-model table before any code, then implement all three classes. The structure mirrors Part A in the inventory domain.*

---

## Part C — Completion Problem

**The problem:** Build authentication for a healthcare scheduling system. Domain participant: `Patient` (patientId, name). Because healthcare data carries HIPAA obligations, the threat-model answer matters more, but the design shape is identical to the library.

**Step 1 — Write the threat-model table first.**

| Threat | Plaintext system | Hashed system |
| --- | --- | --- |
| File read | All patient passwords exposed; HIPAA breach exposure | Dictionary attack required; strong passwords safe |
| Application compromise | Attacker logs in as any patient/provider | Same as file read |
| Credential reuse | Patients' other accounts at risk | Damage limited to weak passwords |

*Why:* The **threat model** is the spec. Healthcare raises the *severity* of the answer (HIPAA), not the design shape.

**Step 2 — Model Patient separately from the credential.**

```java
public class Patient {
    private String patientId;
    private String name;
    // constructor, getters — NO passwordHash field
}
```

*Why:* The credential must be kept separate from the medical record: the fields a doctor reads are not the fields authentication touches.

**Step 3 — [BLANK] Write the UserAccount class.**
*Your work here:* ________________________________________________
(Fields: `username`, `passwordHash`, `patientId` by ID; constructor hashes the password with the chapter's `hash` method; `checkPassword` hashes the supplied password and compares.)

*Why (your explanation):* ________________________________________________

**Step 4 — [BLANK] Write the LoginManager class.**
*Your work here:* ________________________________________________
(A `HashMap<String, UserAccount>`; `addAccount`; a `login` that gets the account, returns `false` if null, else returns `checkPassword`.)

*Why (your explanation):* ________________________________________________

**Step 5 — Trace and verify separation.** Trace `login("pat01", "clinic2024")` through `get` → `checkPassword` → hash comparison → boolean. Confirm authentication never retrieves the `Patient` object and `login` returns only a boolean.
*Why:* Authentication and domain-data access are separate operations; the `Patient` is looked up later by `patientId` only after login succeeds.

**Final answer:** `Patient` (Person), `UserAccount` (credential, `patientId` by ID, SHA-256 hashed), `LoginManager` (HashMap, returns boolean). Threat model written first; HIPAA raises the severity of the file-read row.

**Self-explanation prompt:** Explain why the *design* of the scheduling auth system is identical to the library's even though the *stakes* of a credential exposure are far higher.

---

## Part D — Error-Recognition Problem

> **Use this section only after completing Parts A–C.**

A student implements the library auth system. Their write-up:

**Step 1 (correct).** Threat-model table written; file-read row shows plaintext exposes all passwords, hashed requires a dictionary attack.

**Step 2 (correct).** `Patron` has no credential field; `UserAccount` and `LoginManager` are separate classes.

**Step 3 ⚠.** "To make the code cleaner, I stored a `Patron` object directly in `UserAccount` instead of a `patronId` string: `private Patron patron;`. Now after `login` succeeds I can immediately do `account.getPatron()` and show the borrowing history without a second lookup. This is more convenient and still compiles, so the separation is preserved."

**Step 4 (correct-looking).** The student hashes the password correctly and `login` returns a boolean. The demo passes — correct credentials accepted, wrong rejected — a plausible-looking result.

**Your tasks:**

1. **Identify and explain the error in Step 3.** Storing a `Patron` *reference* in `UserAccount` (instead of the `patronId` string) breaks the separation of concerns. Now every piece of code that touches authentication also has access to the patron's borrowing history; the security surface that should be confined to credentials now reaches into business data. "It compiles" and "the demo passes" do not mean the separation is preserved — the coupling is structural, not behavioral.

2. **Write the corrected Step 3.** "`UserAccount` stores `private String patronId;`, not a `Patron` reference. After `login` succeeds, the calling code performs a *separate* lookup with `patronId` to retrieve the `Patron`. Authentication and domain-data access stay distinct."

3. **State the principle violated.** The chapter's rule that the `UserAccount` stores a *key*, not an *object reference* — `patronId` links to the patron without embedding it — so that authentication code never carries domain data.

4. **Design a test to catch this class of error.** Add a feature that requires iterating all patrons (e.g., a librarian report). With the `Patron` reference embedded in `UserAccount`, the patron list is now reachable from the credential layer, and you will find authentication code with access to every patron's history. The test: grep for any method on the auth path that can reach `Patron` business getters — none should exist. The `patronId`-only design passes; the embedded-reference design fails.

**Why this error is common:** Embedding the object reference is genuinely *more convenient* (no second lookup), so students trade away separation of concerns for a one-line saving without noticing the security surface they just widened.

---

## Part E — Transfer Problem

**The problem (different domain — an online exam proctoring system, not the chapter's library/inventory/scheduling trio):** Students log in to take exams. The domain participant is `Examinee` (examineeId, name, enrolled-course list). Build the separated, hashed design: a **threat model** table (what does a file read expose — and note that exam credentials could let an attacker submit answers as another student), an `Examinee` with no credential field, a `UserAccount` storing `examineeId` *by ID* with a SHA-256 `passwordHash` and `checkPassword`, and a `LoginManager` over a `HashMap` whose `login` returns a boolean and never returns the `Examinee`.

**Hint (use only if stuck after 10 minutes):** Map the three objects directly: `Examinee`=Person, `UserAccount`=credential (link by `examineeId`, hash the password), `LoginManager`=HashMap directory returning boolean. The threat-model question is identical; only the severity of the answer changes.

**Reflection prompt:** (1) What made it possible to transfer the library auth design to exam proctoring with no new concepts? (2) Which property of the design would you point to if a teammate proposed storing the plaintext password "just for the prototype"?

---

## Part F — Interleaved Review

**Problem F1.** A teammate's `LoginManager.login` returns an enum (`LOGIN_SUCCESS`, `USER_NOT_FOUND`, `WRONG_PASSWORD`) so the UI can show a specific error. Apply the threat-model habit: what does this expose to an attacker, what does the UI gain, and what is your recommendation?
*Chapter this draws from: Chapter 6 (Basics of GUI Programming in Java — threat model; authentication; information leakage / username enumeration).*

**Problem F2.** A `Catalog` of `Book` entities is preloaded in `main`, and a `LoginManager` is built afterward. A teammate wants the `Catalog` to hold a `currentUser` field so it "knows who is searching." Explain why this violates supply-side separation and how the separation test would reveal it.
*Chapter this draws from: Chapter 5 (Inheritance and Polymorphism — entity vs. transaction; supply-side separation; separation test).*

**Problem F3 (discrimination).** A `UserAccount` stores a `patronId` string correctly, but after login the app calls `catalog.findByPatron(account)` and the catalog stores a reference to the account to "remember the session." A student says "this is an authentication bug — the credential is leaking." Decide whether the defect is an authentication separation problem (Chapter 6) or a supply-side modeling problem (Chapter 5), and justify which chapter's rule it violates first.
*Note to instructor: intentionally ambiguous — the surface cue is the `UserAccount`/credential (Chapter 6), but the actual defect is the *catalog* (a supply-side entity collection) holding a reference toward a session/transaction object, which is the Chapter 5 supply-side separation failure.*

**After F1–F3:** Write two sentences naming the cue that pulled you toward the wrong chapter in F3 and how you decided which rule was violated first.

---

## Instructor Notes

**Common errors to watch for:**
- Storing the plaintext password in a field named `passwordHash` (e.g., `this.passwordHash = password`) — the demo passes identically, so the bug is invisible without the threat model.
- Embedding a `Patron`/`Employee`/`Patient` *reference* in `UserAccount` instead of the ID string (the Part D error), widening the security surface.
- Hashing on storage but comparing the *raw* supplied password on verification (or vice versa), so the comparison can never match — or matches the wrong thing.

**Signs a student needs to return to the chapter:**
- They cannot state, on their own design, what a file read would expose — i.e., they wrote code before the threat-model table.
- Their `login` returns the `UserAccount` or the domain participant rather than a boolean, blurring authentication with the lookup that should follow it.

**Scaffolding adjustments:** If a student struggles with Part A, have them write only the threat-model table first and predict, line by line, what a plaintext vs. hashed file read exposes before writing any class. If a student finishes Part F quickly, have them design the persistence of the account directory (Challenge exercise) and name why moving from an in-memory `HashMap` to a stored file would change the `UserAccount` or `LoginManager` interface.

**Domain adaptation note:** Swap `Patron` for the student's project participant (`Employee`, `Patient`, `Examinee`) — the Person/UserAccount/LoginManager separation, SHA-256 hashing, and threat-model-before-code discipline are identical across domains; only the participant class and the *severity* of the threat-model answer change.
