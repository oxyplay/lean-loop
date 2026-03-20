# TDD Execution Rules

## 1. The Red-Green-Refactor Loop
- **RED:** Write ONE test for ONE behavior. Ensure it fails. 
  > **Important:** Always wait for console output from the user.  
  > Exception: If the test was just run in this session and the full log is already in context, you may interpret the error. Never guess tracebacks from memory.
- **GREEN:** Write only the minimal code required to make the test pass. No future-proofing or extra features.
- **REFACTOR:** Improve design (deepen modules, remove duplication) **only** when the test is green.

## 2. Test Design Principles
- **Behavior over Implementation:** Test public interfaces. Avoid mocking internal collaborators or private methods.
- **Integration-Style:** Exercise real code paths. Tests should survive internal refactors.
- **System Boundaries:** Only mock external APIs, Databases, Time, or Randomness.

## 3. Architecture Goals
- **Deep Modules:** Aim for small interfaces that hide complex implementations.
- **Dependency Injection:** Accept dependencies; do not create them internally.
- **Vertical Slices:** Use "Tracer Bullets" — complete one end-to-end path at a time.

## 4. Exceptions (When to break TDD)
In rare cases, strict TDD may be skipped. These cases include:
1. **Hotfixes (Production bugs):** When immediate system recovery is critical (write tests later).
2. **Legacy Code:** When the code is too tightly coupled and writing tests would require massive refactoring.
3. **Spikes (Exploratory code):** For hypothesis validation or proof-of-concept that will be thrown away later.

> **Mandatory Rule:** Any exception must be documented in `.system/LOG.md` with the reason for deviating from TDD.
