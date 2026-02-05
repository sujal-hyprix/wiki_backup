---
title: software-verification
description: 
published: true
date: 2026-02-03T06:02:54.707Z
tags: 
editor: markdown
dateCreated: 2026-02-03T06:02:53.655Z
---

# Avionics Software Verification

## 1. Overview
Software Verification is the technical assessment of the software to ensure correctness, consistency, and completeness. In DO-178C, verification is not an activity performed only at the end of the project; it is an integral process that runs concurrently with development.

**The Golden Rule:** You cannot test quality into a product at the end; you must build it in. However, verification provides the *proof* required for certification.

## 2. The Three Methods of Verification
DO-178C verification relies on a triad of activities. You cannot rely on testing alone.

| Method | Purpose | Application |
| :--- | :--- | :--- |
| **Reviews** | Qualitative assessment. Used to ensure artifacts are correct and follow standards. | Plans, Requirements, Design, Source Code, Test Cases. |
| **Analyses** | Quantitative/Repeatable assessment. Used for properties that cannot be tested dynamically. | Stack usage, Worst-Case Execution Time (WCET), Code Coverage, Memory margins. |
| **Tests** | Execution of the software to find errors. | Executable Object Code (EOC) running on target hardware. |

---

## 3. Independence
For safety-critical software (Level A and B), DO-178C requires **Independence**.
*   **Definition:** The person verifying the item must not be the person who developed it.
*   **Why?** Developers have "blind spots" regarding their own errors. Independence removes bias.
*   **Application:**
    *   **Level A:** Required for most verification objectives (Reviews, Test development, Coverage Analysis).
    *   **Level B:** Required for many, but fewer than Level A.

---

## 4. Requirements-Based Testing (RBT)
In avionics, we do **not** do "ad-hoc" testing. All testing is driven by requirements.

### 4.1 Normal Range Testing
Tests that input valid data to ensure the software responds exactly as the High-Level Requirements (HLR) and Low-Level Requirements (LLR) specify.
*   **Equivalence Class Partitioning:** Grouping inputs that should behave similarly and testing one from each group.
*   **Boundary Value Analysis:** Testing the edges of the ranges (e.g., if valid is 0-100, test 0, 100, and 50).

### 4.2 Robustness Testing
Tests that input **invalid** or **unexpected** data to ensure the software does not crash or corrupt data.
*   **Examples:** Division by zero, null pointers, inputs outside valid ranges (e.g., -1 or 101), hardware failures.
*   **Goal:** The software must fail gracefully or handle the error as defined in the requirements.

---

## 5. Verification of Verification (Structural Coverage)
Once testing is complete, we must ask: "Did we test everything?" This is answered via **Structural Coverage Analysis**. We instrument the code to see which lines were executed during testing.

**Coverage Criteria by Level:**
*   **Level C (Statement Coverage):** Every line of code was executed at least once.
*   **Level B (Decision Coverage):** Every decision (e.g., `if (A or B)`) has taken both True and False outcomes.
*   **Level A (MC/DC - Modified Condition/Decision Coverage):** The most rigorous standard. You must prove that *every* condition within a decision independently affects the outcome.
    *   *Example:* In `if (A and B)`, you must show that changing A alone changes the result, AND changing B alone changes the result.

**Addressing Gaps:**
If code is found that was *not* covered by tests, it falls into one of three categories:
1.  **Missing Test:** The feature exists in requirements but we forgot to write a test. -> *Action: Write the test.*
2.  **Extraneous Code:** The code exists but there is no requirement for it. -> *Action: Remove the code (it is a hazard).*
3.  **Dead Code:** Code that cannot be executed (e.g., `if (false)`). -> *Action: Remove the code.*

---

## 6. Required Analyses
In addition to dynamic testing, specific engineering analyses must be performed and documented:
1.  **WCET (Worst-Case Execution Time):** Mathematical proof that the software will always finish its task within its time slice, even under the worst possible scenario.
2.  **Stack Analysis:** Proof that the memory stack will never overflow.
3.  **Data & Control Coupling:** Analysis proving that software modules affect each other *only* as intended by the design.
