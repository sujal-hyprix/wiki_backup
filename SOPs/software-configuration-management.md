---
title: software-configuration-management
description: 
published: true
date: 2026-02-03T06:14:56.484Z
tags: 
editor: markdown
dateCreated: 2026-02-03T06:14:55.503Z
---

# Avionics Software Configuration Management (SCM)

## 1. Overview
Software Configuration Management (SCM) in DO-178C is not just about version control. It is the discipline of identifying, organizing, and controlling modifications to the software to ensure **integrity**, **traceability**, and **reproducibility**.

**The Golden Rule of SCM:** You must be able to regenerate the exact executable object code (the binary that flies) from the source files 20 or 30 years after the original certification [7].

---

## 2. Data Control Categories (CC1 vs. CC2)
DO-178C distinguishes between two levels of rigor for configuration management.

| Category | Rigor Level | Applied To | Requirements |
| :--- | :--- | :--- | :--- |
| **CC1 (Control Category 1)** | **High** | Critical artifacts: Source Code, Executable Object Code, Requirements, Design, SCI, PSAC. | • Configuration Identification<br>• Baselines<br>• Traceability<br>• Problem Reporting<br>• Change Control (CCB)<br>• **Archive/Retrieval protection** |
| **CC2 (Control Category 2)** | **Low** | Supporting artifacts: Test Results, Problem Reports, SQA Records. | • Configuration Identification<br>• Traceability<br>• Change Control<br>• Archive/Retrieval |

*Note: CC1 requires a formal Problem Report and Change Control Board (CCB) approval to modify a file once baselined. CC2 allows for a slightly less formal update process.* [1, 8]

---

## 3. The Change Management Loop
Once an artifact (like a Requirement or Source Code file) is **Baselined**, it cannot be changed without a formal process.

1.  **Problem Reporting:** Anyone identifying a bug or enhancement must file a **Problem Report (PR)**.
2.  **Change Control Board (CCB):** A group of stakeholders (Engineering, QA, Safety) reviews the PR. They decide if the change is necessary and safe.
3.  **Change Impact Analysis (CIA):** Before touching the code, you must analyze *traceability* to determine the "Ripple Effect."
    *   *If I change this line of code, which LLRs are affected?*
    *   *Which tests must be re-run (Regression)?* [6]
4.  **Implementation & Verification:** The change is made and verified.
5.  **Re-Baseline:** The artifact is updated and a new version number is assigned.

---

## 4. Critical Deliverables: The Indices
SCM produces two documents that define the "Configuration" of the product.

### 4.1 Software Configuration Index (SCI)
The SCI is the "parts list" for the software. It identifies the configuration of the software product that is approved for flight.
*   **Contents:** Part numbers of the Executable Object Code, Source Code files, and the specific **Build Instructions** used to compile/link them.
*   **Purpose:** It proves exactly what is on the aircraft [4].

### 4.2 Software Life Cycle Environment Configuration Index (SLECI)
The SLECI defines the "kitchen" used to cook the software.
*   **Contents:** Identifies the tools (compiler version, linker, test tools), hardware, and operating system used to develop and verify the software.
*   **Purpose:** Ensures that if we need to re-compile the code in 10 years, we can recreate the exact environment (same compiler version, same flags) to get the same binary result [2].
