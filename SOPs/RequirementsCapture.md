---
title: Avionics Software Requirements Capture Process
description: 
published: true
date: 2026-02-02T06:59:44.101Z
tags: 
editor: markdown
dateCreated: 2026-02-02T06:59:41.975Z
---


# Avionics Software Requirements Capture Process

## 1. Overview & Planning
Before requirements capture begins, the project scope and safety rigor must be defined. Software does not exist in a vacuum; it is part of the larger  system.

*   **Determine Software Level (DAL):** The criticality of the software is determined by the System Safety Assessment (PSSA) based on failure conditions.
    *   **Level A (Catastrophic):** Highest rigor, requires independence.
    *   **Level B (Hazardous/Severe):** High rigor.
    *   **Level C (Major):** Moderate rigor.
    *   **Level D (Minor):** Low rigor.
*   **The 5 Core Plans:** No work begins until the following plans are drafted:
    1.  **PSAC:** Plan for Software Aspects of Certification (Certification strategy).
    2.  **SDP:** Software Development Plan (How we build it).
    3.  **SVP:** Software Verification Plan (How we test/review it).
    4.  **SCMP:** Configuration Management Plan (How we control changes).
    5.  **SQAP:** Quality Assurance Plan (How we ensure compliance).

---

## 2. Inputs Required (Gathering Phase)
We do not invent software requirements; we derive them from system-level data. You must request and analyze the following inputs before writing High-Level Requirements (HLRs).

| Input Source | Deliverable Needed | Purpose |
| :--- | :--- | :--- |
| **Project Lead** | **System Requirements Data (SRD)** | Defines algorithms, logic, and system functions allocated to software. |
| **Safety Team** | **PSSA / Safety Assessment** | Identifies safety-critical functions, redundancy needs, and partition requirements. |
| **Hardware Team** | **Hardware Interface Description** | Defines memory maps, processor limitations, and timing constraints. |
| **GNC / Propulsion** | **Interface Control Documents (ICD)** | Defines bit-level data formats, scaling, units, and I/O timing. |

**Critical Action:** Analyze these inputs for maturity. If the system requirements are ambiguous or incomplete, **do not guess**. Generate a Problem Report (PR) against the system requirements and send it back to the Systems Team.

---

## 3. The Capture Process (Writing Requirements)
The Requirements Capture process translates System Requirements into Software Requirements.

### Step 3.1: Define Granularity (HLR vs. LLR)
DO-178C requires a two-level hierarchy to separate "what" the software does from "how" it does it.

1.  **High-Level Requirements (HLR):**
    *   **Source:** Derived directly from System Requirements.
    *   **Content:** "Black Box" description. Describes inputs, outputs, and functions without describing internal architecture (e.g., "The software shall display altitude").
2.  **Low-Level Requirements (LLR):**
    *   **Source:** Derived from HLRs during the Design Phase.
    *   **Content:** "White Box" description. Describes *how* to code it (e.g., "The function shall read register 0x40, scale by 0.5, and store in variable Alt_Ft").

### Step 3.2: Requirements Attributes
Every requirement written in the Software Requirements Document (SWRD) must possess the following attributes:
*   **Unique Identifier:** A unique tag (e.g., `SW-REQ-001`) for traceability.
*   **Rationale:** Explains *why* the requirement exists. This is crucial for future maintainers and safety auditors.
*   **Traceability:** A direct link pointing back to the parent System Requirement.
*   **Verifiable:** It must be testable. Avoid vague terms like "user-friendly" or "minimize".

### Step 3.3: Derived Requirements
If you add a requirement that does not trace to a System Requirement (e.g., a buffer clearing routine needed for software stability), it is a **Derived Requirement**.
*   **Action:** You must flag it as "Derived" and submit it to the Safety Team for analysis to ensure it does not introduce new hazards.

---

## 4. Post-Capture: Verification & Validation
Once requirements are drafted, they must be verified before coding begins. This prevents the "Snowball Effect" of errors growing larger later in the project.

1.  **Peer Reviews (Verification):**
    *   Conduct a formal review using a checklist.
    *   Check for: Ambiguity, Completeness, Verifiability, and Conformance to Standards.
    *   *Independence:* For Level A/B software, the reviewer must *not* be the author.
2.  **Validation:**
    *   Ensure these are the *right* requirements (i.e., they accurately represent the system needs).
3.  **Baseline:**
    *   Once reviewed and approved, the SWRD is placed under Configuration Management (CM) and baselined.

---

## 5. Change Management (Propagation)
If a deliverable changes after the baseline (e.g., Propulsion changes a thruster logic), you must follow the formal change process.

1.  **Problem Report (PR):** Open a PR or Change Request to document the incoming change.
2.  **Change Control Board (CCB):** The CCB approves the change for a specific software release.
3.  **Change Impact Analysis (CIA):** You must perform a CIA to determine the "ripple effect". Use your **Traceability Matrices** to find:
    *   Which HLRs are affected?
    *   Which LLRs (Design) are affected?
    *   Which Source Code files are affected?
    *   Which Test Cases must be re-run (Regression)?.

---

## 6. Testing, Verification, and Validation
Testing is performed against the *Requirements*, not the code.

### Test Methods
*   **Requirements-Based Testing (RBT):** Tests confirm the software performs the intended function defined in the HLRs.
*   **Normal Range Testing:** Testing inputs within expected limits.
*   **Robustness Testing:** Testing abnormal inputs (null pointers, divide by zero, out-of-range values) to ensure the software handles them safely.

### Structural Coverage (The "Code" Check)
After RBT is complete, we analyze code coverage to find "Dead Code" or intended functionality that was missed by tests.
*   **Level C:** Statement Coverage (Every line executed).
*   **Level B:** Decision Coverage (Every True/False branch taken).
*   **Level A:** MC/DC (Modified Condition/Decision Coverage) - Verification that every condition independently affects the decision outcome.

### Traceability (The Glue)
You must maintain bidirectional traceability throughout the project:
1.  System Reqs $\leftrightarrow$ Software HLRs
2.  Software HLRs $\leftrightarrow$ Software LLRs (Design)
3.  Software LLRs $\leftrightarrow$ Source Code
4.  Requirements $\leftrightarrow$ Test Cases
