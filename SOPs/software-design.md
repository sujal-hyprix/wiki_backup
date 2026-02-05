---
title: software-design
description: 
published: true
date: 2026-02-02T07:44:40.719Z
tags: 
editor: markdown
dateCreated: 2026-02-02T07:44:39.654Z
---

# Avionics Software Design Process

## 1. Overview
The Software Design phase bridges the gap between **Software Requirements** and **Source Code**. While the requirements phase defines *what* the software must do, the design phase defines *how* the software will implement that functionality.

In DO-178C, "Design" consists of two distinct components:
1.  **Software Architecture:** The high-level structure.
2.  **Low-Level Requirements (LLRs):** The detailed logic from which code can be directly written.

---

## 2. Inputs Required
Before design begins, the following inputs must be available and sufficiently mature:

| Input Artifact | Description |
| :--- | :--- |
| **High-Level Requirements (HLRs)** | The "Black Box" requirements derived from the system. These are the primary driver for the design. |
| **Software Design Standards** | The rules and constraints for the design team (e.g., naming conventions, allowed complexity, prohibited logic constructs). |
| **Interface Control Documents** | Definitions of external hardware and software interfaces that the architecture must accommodate. |

---

## 3. The Design Process
The design process is decomposed into defining the structure (Architecture) and the details (LLRs).

### 3.1 Software Architecture
The architecture is the "blueprint" of the software. It must define the structure of the software components and how they interact.
*   **Components:** The major functional blocks or modules of the software.
*   **Data Flow:** How data moves between components.
*   **Control Flow:** How execution sequencing is managed between components.
*   **Integrity & Availability:** The architecture must implement the safety strategies (e.g., partitioning, redundancy, safety monitors) defined in the requirements.

### 3.2 Low-Level Requirements (LLRs)
This is a concept unique to safety-critical standards like DO-178C. **LLRs are Design.** They are detailed refinements of HLRs written specifically for the coder.
*   **Granularity:** LLRs must be detailed enough that a programmer can write the Source Code without asking for further information.
*   **Focus:** LLRs describe *how* to implement the function (algorithms, specific register usage, internal variable names).
*   **Derived LLRs:** If the design process introduces a requirement not traceable to an HLR (e.g., a loop counter or a buffer management flag), it is a **Derived LLR**. These must be justified and typically do not require safety assessment unless they impact higher-level functionality.

---

## 4. Characteristics of Good Design (Safety Metrics)
To ensure safety and maintainability, the design must adhere to specific technical characteristics. The two most critical metrics are **Coupling** and **Cohesion**.

### 4.1 Coupling (Minimize)
Coupling is the degree of interdependence between two software components. **Loose coupling** is required to minimize the "ripple effect" where a change in one module breaks another. DO-178C explicitly requires analysis of two types:
*   **Data Coupling:** Dependence on data not exclusively under the control of the component (e.g., global variables).
*   **Control Coupling:** One component influencing the execution of another (e.g., one function calling another, or passing a flag that determines the logic path of another).

### 4.2 Cohesion (Maximize)
Cohesion is the "glue" that keeps a component together. **Strong cohesion** is required.
*   **Functional Cohesion (Best):** Every element in the component contributes to a single, specific task.
*   **Coincidental Cohesion (Worst):** Elements are grouped haphazardly (e.g., a "Utilities" file with unrelated math and string functions).

---

## 5. Traceability (The Design Thread)
You must maintain a continuous thread of traceability. You cannot write code that does not trace to an LLR, and you cannot write an LLR that does not trace to an HLR.

**The Trace Flow:**
`System Req` $\rightarrow$ `High-Level Req (HLR)` $\rightarrow$ `Software Architecture` $\rightarrow$ `Low-Level Req (LLR)` $\rightarrow$ `Source Code`

*   **Bidirectional:** You must be able to trace forwards (to see implementation) and backwards (to see rationale/origin).

---

## 6. Outputs & Verification
### 6.1 Output: Software Design Description (SDD)
The primary deliverable is the **Software Design Description (SDD)**. It contains the Architecture definition, the LLRs, and the Trace Data.

### 6.2 Design Verification (Reviews)
Before coding begins, the design must be verified (usually via Peer Review) against **DO-178C Table A-4** objectives.
*   **Checklist Items:**
    1.  **Compliance:** Do LLRs comply with HLRs? (Did we design what was asked?)
    2.  **Traceability:** Is the HLR $\leftrightarrow$ LLR trace complete?
    3.  **Verifiability:** Can the design be tested?
    4.  **Standards:** Does the design follow the Design Standards?
    5.  **Partitioning:** Is the partitioning integrity (separation of critical components) confirmed?
