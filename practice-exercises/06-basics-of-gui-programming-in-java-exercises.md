# Module 6 — GUI Programming: Authentication & Credential Design
## Exercise Set

**Learning Objectives**
1. Separate domain objects from credential objects (Person vs UserAccount)
2. Implement SHA-256 password hashing using `MessageDigest`
3. Design a `LoginManager` with a `HashMap` credential directory
4. Answer threat-model questions about plaintext vs hashed password storage

---

## Worked Example

*Study this example before attempting Tier 1. After reading it, close it and try to recall the key steps from memory before moving on.*

**Problem:** A student writes a login check like this:

```java
public boolean login(String username, String password) {
    UserAccount account = accounts.get(username);
    return account != null && account.password.equals(password);
}
```

Is this correct? Apply the credential security principles from this chapter.

**Approach:**
1. **Identify what is stored.** `account.password` holds the plaintext password — the exact string the user typed at registration. This is the first problem.
2. **Identify what is compared.** `account.password.equals(password)` compares the stored plaintext to the typed input. If an attacker reads the credential store, all passwords are immediately readable.
3. **Apply the SHA-256 principle.** Passwords must never be stored in plaintext. At registration, hash the password with SHA-256 via `MessageDigest` and store only the hash. At login, hash the input and compare hashes:

```java
String inputHash = hashPassword(password);
return account != null && account.passwordHash.equals(inputHash);
```

4. **Check what is returned.** Returning `boolean` is correct — the method should only answer "yes/no," not return the domain object. The `Patron` should be retrieved separately through the catalog after a successful login.

**Answer:** Two problems: (1) plaintext password stored and compared — should store and compare SHA-256 hashes; (2) returning `boolean` is already correct in this version, which is good. The fix is entirely in replacing `account.password` with `account.passwordHash` and hashing the input before comparison.

**What to notice:** The login method is almost right. The single change — hash before storing, hash before comparing — is what separates a vulnerable design from a safe one.

---

## Tier 1 — Warm-Up

*(Tests: recall, vocabulary, true/false with explanation)*

---

**Exercise 1** (Tests: recall — authentication vs authorization)

What is the difference between authentication and authorization? Give one concrete example of each in a library system.

---

**Exercise 2** (Tests: true/false — plaintext password storage)

**True or False:** "Storing passwords as plain text is acceptable for a student project because it is only used internally."

State whether the claim is true or false, then write two to three sentences explaining your answer.

---

**Exercise 3** (Tests: vocabulary — ID-based linking)

Why does a `UserAccount` link to a `Patron` by patron ID rather than by a direct object reference? What security or design property does this separation provide?

---

**Exercise 4** (Tests: recall — SHA-256 properties)

What property of SHA-256 makes it suitable for password storage? Define the term "one-way function" as it applies to password hashing.

---

**Exercise 5** (Tests: true/false — hash collision behavior)

**True or False:** "If two patrons have the same password, their stored hashes will be the same."

State whether the claim is true or false, then explain what this means for an attacker who obtains the credential file.

---

**Exercise 5b** (Tests: plaintext vs. hashed storage vs. domain separation — contrastive classification)

Classify each of the following as an **authentication concern**, a **domain concern**, or **both**. Write one sentence explaining each classification.

- (a) Whether a patron's name is spelled correctly
- (b) Whether the password matches the stored hash
- (c) Which books a patron has currently checked out
- (d) Whether a username already exists in the credential store
- (e) Retrieving the `Patron` object after a successful login

*(Why this is tempting to get wrong: (d) and (b) both involve the credential store — but (d) is about uniqueness/registration, not about checking credentials. The classification depends on which layer of the design each concern belongs to.)*

---

## Tier 2 — Application

*(Tests: scenario design, error analysis, AI interaction)*

---

**Exercise 6** (Tests: threat modeling — plaintext vs hashed)

Complete the threat model table below for two credential storage designs used in a library system. For each design, answer both attacker scenarios.

| | Design A: Plaintext HashMap | Design B: SHA-256 Hashed HashMap |
|---|---|---|
| An attacker reads the saved credential file | | |
| An attacker views the HashMap in memory during a debugger session | | |

After completing the table, write one sentence summarizing which design you would choose and why.

---

**Exercise 7 — Error Analysis** (Tests: error identification — login method design)

A student builds a login system for a library. Their `LoginManager` contains the following method:

```java
public Patron login(String username, String password) {
    UserAccount account = accounts.get(username);
    if (account != null && account.password.equals(password)) {
        return account.patron;  // returns the actual Patron object
    }
    return null;
}
```

Identify **two** security or design problems in this method. For each problem:
- Name the problem
- Explain the specific risk it creates
- Write a corrected version of the relevant line or lines

---

**Exercise 8** (Tests: scenario design — hospital authentication system)

Design a `LoginManager` for a hospital appointment system where patients are represented by `Patient` objects. Write the following:

**(a)** The `UserAccount` class with appropriate fields. The class must not contain a plaintext password field.

**(b)** The `LoginManager` class signature and a `login()` method that returns `boolean` rather than a `Patient` object.

**(c)** A one-paragraph explanation of why `login()` returns `boolean` rather than returning the `Patient` object directly.

---

**Exercise 9 — AI Interaction** (Tests: evaluating AI-generated security advice — hashing requirement)

First, without consulting AI, write one sentence describing what must happen to a password before it is stored in any Java data structure.

Then read this AI response to "How do I store user passwords in Java?":

> "The simplest approach is to store passwords in a `HashMap<String, String>` where the key is the username and the value is the password. You can check passwords with `storedPasswords.get(username).equals(inputPassword)`."

Answer the following:

**(a)** Identify the strongest point in the AI's response (what, if anything, is correct or useful).

**(b)** Identify the security problem the AI's response introduces.

**(c)** Write a corrected three-sentence explanation of how passwords should be stored in Java, suitable for a student who has just learned about `MessageDigest`.

**(d)** State the specific test you would run to verify that a login system is NOT storing plaintext passwords — what would you inspect, and what result would confirm the system is correctly hashing?

---

**Exercise 9b — Self-Explanation** (Tests: ID-based linking — why separation between credential and domain objects matters)

In this chapter, a `UserAccount` links to a `Patron` by storing `patronId` (a String) rather than by holding a direct `Patron` reference. Explain in 2–3 sentences why ID-based linking is preferable to holding a direct reference. Your explanation must use the term **"credential store"** correctly and explain what would break if a `Patron` object were replaced or reloaded.

---

**Exercise 9c — Cumulative** (Tests: authentication gate + setter-before-show from Ch 3)

In Ch 3, you learned the setter-before-show contract: data must be set on a screen before calling `layout.show()`. In this chapter, an authentication gate must verify a user before granting access to any protected screen.

A library app's login screen calls `LoginManager.login(username, password)`. If it returns `true`, the app navigates to the patron dashboard.

(a) Apply the setter-before-show contract: what must be set on the patron dashboard before `layout.show()` is called?
(b) Where does that data come from — the `LoginManager`, the catalog, or somewhere else?
(c) What specific failure occurs if the dashboard is shown before the patron object is set? Name the object that will be null and the exception that will be thrown.

---

**Exercise 10** (Tests: HashMap design — credential directory structure)

A university course registration system needs to authenticate students. Students are represented by `Student` objects with fields `studentId`, `name`, and `major`.

**(a)** Write the `HashMap` declaration for the credential directory.

**(b)** Explain why the key should be a username `String` rather than a `Student` object reference. What would go wrong if a `Student` object were used as the key?

---

## Tier 3 — Synthesis

*(Tests: cross-chapter integration — must name prior chapters explicitly)*

---

**Exercise 11** (Tests: Ch 6 + Ch 5 — supply-side model and ID-based linking)

*This exercise connects Module 6 with Module 5.*

In Chapter 5, you designed a supply-side catalog where entities — such as `Book` or `Patron` objects — are preloaded before any transactions run. In Chapter 6, a `UserAccount` links to a domain participant (such as a `Patron`) by ID rather than by direct reference.

Explain how these two principles connect by answering the following:

- How does the supply-side model from Chapter 5 ensure that a `UserAccount`-to-`Patron` link works correctly at login time?
- What specific runtime failure occurs if the `Patron` catalog has not been loaded before a user attempts to log in?
- Why is ID-based linking useless if the entity it points to does not yet exist in memory?

A strong answer uses supply-side vocabulary from Chapter 5 (entities, preloading, independence) and explains the specific failure mode, not just a general warning about ordering.

---

**Exercise 12** (Tests: Ch 6 + Ch 3 — setter-before-show and authentication gates)

*This exercise connects Module 6 with Module 3.*

In Chapter 3, you learned the setter-before-show contract: a screen must not be displayed until its required object has been set. In Chapter 6, the authentication system must verify a user before granting access to any protected screen.

Describe how these two principles work together in a login flow by answering the following:

**(a)** Which screen is shown before authentication, and why does it not require a domain object to be set?

**(b)** What state must be set — and by what event — before any protected screen is accessible?

**(c)** What happens at runtime if a developer bypasses the login check and navigates directly to a protected screen? Name the specific object that will be missing or null.

A strong answer applies setter-before-show vocabulary from Chapter 3 and connects it to authentication as a precondition for screen access, not just as a general security concern.

---

## Tier 4 — Challenge

*(No answer key. Rubric only.)*

---

**Exercise 13** (Tests: SHA-256 limitations — attack reasoning from first principles)

SHA-256 hashing prevents an attacker from reading passwords directly from storage. It does not prevent all attacks.

Describe **two** specific attack types that SHA-256 alone does not defend against. For each attack:

- Explain how the attack works mechanically
- Explain why plain SHA-256 is insufficient to stop it
- Describe the additional technique that would mitigate it

You may draw on concepts from outside this chapter. This question asks you to reason from what the hash function does and does not guarantee — not to recall a memorized list.

**Rubric — a strong response will:**
- Correctly explain the mechanism of each attack (not just name it)
- Demonstrate understanding of what SHA-256 guarantees (deterministic, one-way, fixed-length output) and what it does not (uniqueness per user, time cost)
- Propose a concrete mitigation for each attack with a clear explanation of why it works (e.g., salting prevents rainbow table precomputation; key stretching increases brute-force cost)
- Avoid vague mitigations such as "use better security" or "encrypt the hash"

---

## Full Answer Key

*(Tiers 1–3 only)*

---

### Tier 1 Answers

**Exercise 1**
Authentication is the process of verifying who a user is — confirming their identity. Authorization is the process of determining what an authenticated user is allowed to do.

Library examples:
- Authentication: A patron enters their library card number and PIN to log in. The system checks whether those credentials match a known account.
- Authorization: Once logged in, a librarian account can add new books to the catalog, but a patron account cannot.

---

**Exercise 2**
**False.**

Even for internal or student projects, storing plaintext passwords creates serious risk. If the credential file is read — by another student, a curious user, or any process with file access — all passwords are immediately exposed with no further effort. Users commonly reuse passwords across systems, so a breach of a "harmless" project can expose accounts on other services. The correct practice is to hash passwords before storing them, which costs very little additional effort.

---

**Exercise 3**
A `UserAccount` links to a `Patron` by ID rather than by object reference to enforce separation between the credential system and the domain system. The `Patron` object may be updated, replaced, or reloaded from file without invalidating the `UserAccount`. Storing a direct reference would couple the two objects tightly — if the `Patron` object is ever rebuilt (e.g., after loading from CSV), the stored reference becomes stale. ID-based linking also means the credential store does not need to hold any domain data about the patron, which limits how much information is exposed if the credential store is compromised.

---

**Exercise 4**
SHA-256 is a one-way function: given a password, it produces a fixed-length digest, but given the digest, it is computationally infeasible to reconstruct the original password. This makes it suitable for password storage because the stored value can be used to verify a login attempt (hash the input and compare) without ever storing or transmitting the original password. A one-way function is a function where the forward computation is fast and the reverse computation is practically impossible.

---

**Exercise 5**
**True** — SHA-256 is deterministic, so the same input always produces the same output. Two patrons with the password `"sunshine"` will have identical hashes stored.

For an attacker, this is useful: if they recognize that two hashes are identical, they learn that two accounts share a password. More importantly, if they crack one account's password, they have cracked both simultaneously. This is one reason why salting (adding a unique random value to each password before hashing) is used in production systems — salting ensures that identical passwords produce different hashes.

---

### Tier 2 Answers

**Exercise 6**

| | Design A: Plaintext HashMap | Design B: SHA-256 Hashed HashMap |
|---|---|---|
| Attacker reads the credential file | Attacker immediately has all usernames and passwords in readable form. No further work required. | Attacker has hashes, not passwords. They cannot log in with a hash directly. They must attempt to reverse the hash, which requires brute force or precomputed tables. |
| Attacker views the HashMap in memory during a debugger session | Attacker sees all passwords as readable strings directly in memory. | Attacker sees hashed values. Without knowing the original passwords, they cannot use the hashes to determine credentials (though they could potentially copy hashes for offline attack attempts). |

Design B is the correct choice because it ensures that even full read access to the credential store does not immediately yield usable passwords.

---

**Exercise 7**

**Problem 1: Plaintext password comparison**
The field `account.password` stores the password as plain text, and the comparison `account.password.equals(password)` compares plain text directly. If the credential store is ever exposed, all passwords are readable.

Corrected: The stored value should be the SHA-256 hash of the password. The comparison should hash the input before comparing:
```java
String inputHash = hashPassword(password);
if (account != null && account.passwordHash.equals(inputHash)) { ... }
```

**Problem 2: Returning the domain object from login()**
The method returns the actual `Patron` object on success. This means the calling code receives a mutable reference to the domain object via the authentication path. The login method should return only enough information for the caller to proceed — typically a `boolean` or a session token — and the caller should retrieve the domain object through the domain layer separately.

Corrected:
```java
public boolean login(String username, String password) {
    UserAccount account = accounts.get(username);
    if (account == null) return false;
    String inputHash = hashPassword(password);
    return account.getPasswordHash().equals(inputHash);
}
```

---

**Exercise 8**

**(a)** `UserAccount` class:
```java
public class UserAccount {
    private String username;
    private String passwordHash;  // SHA-256 hash, never plaintext
    private String patientId;     // links to Patient by ID, not reference

    public UserAccount(String username, String passwordHash, String patientId) {
        this.username = username;
        this.passwordHash = passwordHash;
        this.patientId = patientId;
    }

    public String getPasswordHash() { return passwordHash; }
    public String getPatientId() { return patientId; }
}
```

**(b)** `LoginManager` signature and `login()`:
```java
public class LoginManager {
    private HashMap<String, UserAccount> accounts = new HashMap<>();

    public boolean login(String username, String password) {
        UserAccount account = accounts.get(username);
        if (account == null) return false;
        String inputHash = hashPassword(password);
        return account.getPasswordHash().equals(inputHash);
    }

    private String hashPassword(String password) {
        // SHA-256 via MessageDigest
        ...
    }
}
```

**(c)** Explanation:
`login()` returns `boolean` rather than a `Patient` object because the authentication layer and the domain layer should be separate. The `LoginManager`'s only responsibility is to confirm that the credentials are valid. Once authentication succeeds, the calling code can retrieve the `Patient` object from the domain catalog using the patient ID stored in the `UserAccount`. Returning the `Patient` directly from `login()` would couple the credential system to the domain model, require the `LoginManager` to hold a reference to the patient catalog, and risk exposing the domain object through a security boundary that should only answer yes or no.

---

**Exercise 9**

**(a)** Strongest point: Using a `HashMap<String, String>` with username as key is correct for fast lookup — O(1) average case — and the key-based design is sound.

**(b)** Security problem: Storing passwords as plain `String` values means any read access to the map (in memory, in a file, or via a debugger) exposes all passwords immediately. The AI recommended storing the password itself, not a hash of it.

**(c)** Corrected explanation:
Passwords should never be stored as plain text. Instead, before storing, compute the SHA-256 hash of the password using `MessageDigest` and store only the hash. At login time, hash the user's input the same way and compare the two hashes — if they match, the password is correct. This way, even if the credential store is read by an attacker, they see only hashes and cannot recover the original passwords directly.

---

**Exercise 10**

**(a)** Declaration:
```java
HashMap<String, UserAccount> credentialDirectory = new HashMap<>();
```

**(b)** The key must be a `String` username rather than a `Student` object reference for two reasons. First, `HashMap` lookup depends on `hashCode()` and `equals()`. If `Student` does not override these methods, Java uses object identity (memory address), meaning two `Student` objects with the same `studentId` would not match as equal keys. Second, using an object reference as a key creates coupling between the credential store and the domain object — if the `Student` object is rebuilt (e.g., after loading from file), the old key no longer maps to the correct entry. A `String` username is stable, self-contained, and does not depend on object identity.

---

### Tier 3 Answers

**Exercise 11**
In Chapter 5, the supply-side catalog preloads all `Patron` objects into memory before any transactions — such as checkout — are allowed to run. The catalog acts as the authoritative in-memory registry of all domain participants. This preloading is what makes ID-based linking in Chapter 6 viable: a `UserAccount` stores a `patronId` string, and after a successful login the application looks up `catalog.findById(patronId)` to retrieve the actual `Patron` object.

If the `Patron` catalog has not been loaded before login is attempted, the lookup returns `null` even though authentication succeeded. The user has proved their identity, but the application cannot find the domain object they are linked to. This is a specific, testable failure: `catalog.findById(account.getPatronId())` returns `null`, and any subsequent code that calls methods on the returned object throws a `NullPointerException`. The authentication step and the domain lookup step are separate operations, and the supply-side model must complete before the domain lookup is meaningful.

> **Common error:** A surface answer says "load the patron data first." A strong answer names the specific failure mode — `catalog.findById()` returns `null` because the in-memory registry is empty — and uses supply-side vocabulary: preload, entities, catalog independence.

---

**Exercise 12**

**(a)** The login screen is shown before authentication. It does not require a domain object to be set because it is not a protected screen — its only purpose is to collect credentials. It has no dependency on a `Patron` or `UserAccount` being present before it is displayed.

**(b)** A protected screen — such as a patron dashboard or checkout screen — requires a successfully authenticated `UserAccount` and a resolved domain object (e.g., the current `Patron`) to be set before it is shown. This state is set by the login event: when `LoginManager.login()` returns `true`, the application resolves the patron from the catalog and calls the setter on the next screen before calling `setVisible(true)`. This is the setter-before-show contract from Chapter 3 applied at the authentication boundary.

**(c)** If a developer bypasses the login check and navigates directly to the patron dashboard, the screen's `currentPatron` field will be `null` — it was never set because the login event never fired. Any method on that screen that calls `currentPatron.getName()` or similar will throw a `NullPointerException`. The screen will appear to open but will immediately crash when it tries to display patron data. The setter-before-show contract and the authentication gate enforce the same underlying requirement: the screen must not be displayed before the object it depends on has been provided.

> **Common error:** A surface answer treats authentication as purely a security concept and misses the structural connection. A strong answer names `currentPatron` as the missing object, identifies `NullPointerException` as the failure, and explicitly uses "setter-before-show" from Ch 3.

---

## Instructor Notes

**Common errors to watch for:**

- **Exercise 2 / Exercise 7:** Students often accept plaintext storage for "simple" or "internal" projects. Push back on this framing — the habit of hashing is as important as the technique itself.

- **Exercise 7:** The "returning the domain object" problem is frequently missed. Students focus on the hashing issue and overlook the architectural separation issue. Both should be required for full credit.

- **Exercise 8c:** Weak answers say only "for security." A strong answer identifies the specific coupling problem — the `LoginManager` would need to hold a catalog reference — and names the separation of concerns principle.

- **Exercise 11:** Students who did not internalize the supply-side model from Chapter 5 will give vague answers about "loading data first." Require them to use the words "preload," "entities," and "catalog" and to name the specific null failure.

- **Exercise 12:** Watch for answers that treat authentication only as a security concern and miss the setter-before-show connection entirely. The question requires them to use Chapter 3 vocabulary explicitly.

- **Exercise 13 (Challenge):** Common weak responses name "dictionary attack" and "rainbow table" as if they are different categories. A strong response explains that both exploit the deterministic nature of hashing, and that salting breaks precomputation specifically. Credit responses that show understanding of the mechanism, not just the label.

**Point distribution:** T1 = 5 pts each · T2 = 10 pts each · T3 = 15 pts each · T4 = 20 pts (rubric-graded)

**Bloom's distribution:**

| Tier | Bloom's Level | % of exercises |
|------|--------------|----------------|
| Tier 1 | Remember / Understand | ~25% |
| Tier 2 | Apply / Analyze | ~55% |
| Tier 3 | Analyze / Evaluate | ~12% |
| Tier 4 | Evaluate / Create | ~8% |

**DEI note:** Exercise 8 uses a hospital / patient scenario. Be sensitive if students have had stressful healthcare experiences; the technical concepts (boolean return, hash storage) are fully separable from the medical framing.
