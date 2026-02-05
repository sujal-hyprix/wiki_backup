---
title: software-quality-assurance
description: 
published: true
date: 2026-02-03T08:00:05.093Z
tags: 
editor: markdown
dateCreated: 2026-02-03T08:00:03.702Z
---

# Avionics Software Quality Assurance (SQA)

## 1. Overview
Software Quality Assurance (SQA) is the process of providing assurance that the software life cycle processes satisfy the approved plans and standards. While the **Verification** team looks for errors in the *software* (bugs), the **SQA** team looks for errors in the *process* (deviations from the plan).

**The SQA Motto:** Quality must be built into the product; it cannot be inspected into it at the end. SQA ensures the "Recipe" (Plans) was followed to create the "Cake" (Software) [2].

---

## 2. Independence and Authority
In DO-178C, SQA requires a strict form of **Independence**.
*   **Separation of Responsibility:** The SQA engineer cannot be the developer of the item they are auditing.
*   **Authority:** SQA must have the authority to ensure corrective action. If SQA finds a non-compliance, they must have the power to stop the release until it is fixed. SQA typically does not report to the Software Project Manager to avoid conflicts of interest [3].

---

## 3. Key SQA Activities
SQA is an active participant throughout the life cycle, not just at the end.

### 3.1 Audits of Life Cycle Data
SQA audits the artifacts (requirements, code, test results) to ensure they were produced in accordance with the **Plans** (PSAC, SDP) and **Standards** (Requirements, Design, and Coding Standards).
*   *Example:* Did the code review actually happen? Did the reviewers use the checklist? Was the checklist signed? [5].

### 3.2 witnessing
SQA witnesses critical events to ensure they are repeatable and follow procedures.
*   **Test Witnessing:** SQA watches the verification team run tests to ensure they follow the test procedures and do not "fudge" the results [6].
*   **Build/Load Witnessing:** SQA witnesses the software build (compilation) and load to ensure the environment matches the **Software Life Cycle Environment Configuration Index (SLECI)** [6].

### 3.3 Transition Criteria Assessment
SQA ensures that a phase does not close until it is actually done. They check the **Transition Criteria** (defined in the plans) to prevent the project from moving to the next phase prematurely (e.g., preventing coding before design is reviewed) [6].

---

## 4. The Software Conformity Review
The **Conformity Review** is the final SQA activity before the software is submitted for certification. It is a comprehensive audit that produces the **Software Conformity Review Report**.

**Conformity Checklist:**
1.  **Completeness:** Are all life cycle data (plans, code, tests) generated and complete?
2.  **Traceability:** Does the system trace from top (System Reqs) to bottom (Code/Tests) without gaps?
3.  **Consistency:** Did we follow the plans?
4.  **Problem Reports:** Are all problem reports closed or validly deferred?
5.  **Regeneration:** Can the Executable Object Code be regenerated exactly from the Source Code using the build instructions? [4].
