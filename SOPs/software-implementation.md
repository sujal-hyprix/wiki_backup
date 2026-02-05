---
title: software-implementation
description: 
published: true
date: 2026-02-02T09:02:48.004Z
tags: 
editor: markdown
dateCreated: 2026-02-02T09:02:46.994Z
---

# Avionics Software Implementation: Coding & Integration

## 1. Objective & Scope
The Implementation phase is where the rubber meets the road. It consists of two distinct activities:
1.  **Coding:** Translating the Low-Level Requirements (LLRs) into Source Code.
2.  **Integration:** Compiling, linking, and loading that code into the target hardware to create the Executable Object Code.

**Critical Mindset:** In safety-critical development (DO-178C), coding is not "invention." It is the deterministic translation of the Design (LLRs) into a machine-readable format. If you find yourself inventing logic that isn't in the LLRs, stop. You are deviating from the design.

---

## 2. Prerequisites (Entry Criteria)
You cannot begin formal coding until the following are mature:
*   **Low-Level Requirements (LLRs):** The algorithms and logic must be defined.
*   **Software Architecture:** The structure, interfaces, and data flow must be defined.
*   **Coding Standards:** A checklist of rules (e.g., MISRA-C) that enforces safety constraints.

---

## 3. The Coding Process (Rules & Constraints)
Avionics code differs from standard IT software. It must be **deterministic**, **observable**, and **safe**.

### 3.1 Traceability (The "Golden Thread")
You must maintain a bidirectional link between the LLRs and the Code.
*   **Forward Trace:** Every LLR must have a corresponding piece of code.
*   **Backward Trace:** Every line of code must trace back to an LLR.
*   **Zero Tolerance for "Gold Plating":** You cannot add extra features "just in case." If code exists without a requirement, it is classified as **Extraneous Code** or **Dead Code** and must be removed.

### 3.2 The "Known Troublemakers" (Prohibited Patterns)
To ensure safety, Rierson and DO-178C strongly advise against specific coding structures that introduce unpredictability.

| Feature | Status | Why is it dangerous? |
| :--- | :--- | :--- |
| **Recursion** | **Prohibited** | Functions calling themselves can lead to infinite loops and stack overflow (running out of memory). If used, you must prove a mathematical upper bound on stack usage. |
| **Dynamic Memory** | **Prohibited** | `malloc` / `free` causes memory leaks and fragmentation. All memory should be allocated statically at initialization. |
| **Pointers** | **Restricted** | Incorrect pointer referencing is a leading cause of crashes. If used, they must be strictly controlled and reviewed. |
| **Unbounded Loops** | **Prohibited** | Every loop must have a fixed upper limit to ensure the software doesn't hang (determinism). |
| **Dead Code** | **Remove** | Code that can never be executed (due to logic errors) must be removed. It confuses analysis and wastes resources. |

### 3.3 Robustness & Defensive Programming
You must assume the inputs will eventually be bad.
*   **Input Validation:** Check variables for range tolerance and corruption before using them.
*   **Default Clauses:** Every `switch` or `case` statement *must* have a default clause to handle unexpected states.
*   **Else Statements:** Every `if` should have an `else` to ensure deterministic behavior in all conditions.

---

## 4. The Integration Process (Build & Load)
Integration is not just "running the makefile." It is a formal process of converting Source Code into the binary that flies.

### 4.1 The Build Environment
*   **Controlled Environment:** You must document the exact version of the compiler, linker, and operating system used to build the code. This is stored in the **Software Life Cycle Environment Configuration Index (SLECI)**.
*   **Compiler Settings:** Optimization settings must be documented. Aggressive optimization can sometimes alter the logic of the code, creating a mismatch between source and object code.

### 4.2 The "Clean Build"
You must prove the software can be regenerated from scratch.
*   **Procedure:** Delete all object files, temporary files, and previous binaries. Re-compile and re-link everything from the source.
*   **Repeatability:** If you build the software today, and again in 5 years, the binary output must be *identical*.

### 4.3 Compiler Warnings
*   **Zero Tolerance:** Ideally, the code should compile with **zero warnings**.
*   **Justification:** If a warning cannot be fixed, it must be analyzed to prove it does not impact safety. This analysis must be documented.

### 4.4 The Load Process (Getting it on the Hardware)
*   **Integrity Check:** When loading software onto the target (the aircraft computer), you must verify the load wasn't corrupted. This is usually done via a **Cyclic Redundancy Check (CRC)** or Checksum calculation.
*   **Part Numbering:** The loaded software must report its version/part number so the aircraft configuration can be verified.

---

## 5. Verification of Implementation (Peer Reviews)
Before testing begins, the code is verified via **Peer Review**. We do not just "look it over"; we review against specific DO-178C Table A-5 objectives:

1.  **Compliance:** Does the code actually implement the LLR?
2.  **Conformance:** Does the code follow the **Coding Standards** (naming conventions, headers, complexity limits)?
3.  **Traceability:** Is the Source Code $\leftrightarrow$ LLR trace complete?
4.  **Accuracy & Consistency:**
    *   **Stack Usage:** Will the stack overflow?
    *   **WCET (Worst-Case Execution Time):** Will the code finish running within its time slice?
    *   **Memory Safety:** Are variables initialized before use? Are mathematical overflows prevented?

**Output Artifact:** The **Software Configuration Index (SCI)**. This document lists the specific source files, object files, and build instructions that comprise the final product. It is the "Recipe" for the software.
