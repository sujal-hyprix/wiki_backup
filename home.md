---
title: Home
description: 
published: true
date: 2026-01-29T06:31:22.336Z
tags: 
editor: markdown
dateCreated: 2026-01-29T06:31:19.959Z
---

# 🚀 Avionics & Embedded Systems Engineering Wiki

Welcome to the **Engineering Wiki** for our avionics, guidance, and embedded systems teams.  
This wiki is the **single source of truth** for technical knowledge, processes, standards, and lessons learned across all projects.

---

## 🎯 Purpose of This Wiki

This wiki exists to:

- Standardize **engineering processes** across all programs
- Capture **design rationale** and trade studies
- Document **interfaces** between teams (Avionics, GNC, Structures, Propulsion)
- Preserve **tribal knowledge** and lessons learned
- Support **certification, audits, and reviews**
- Enable faster onboarding of new engineers

> **If it’s not documented here, it doesn’t exist.**

---

## 🧭 Who This Wiki Is For

- Avionics Hardware Engineers  
- Avionics Software Engineers  
- GNC Engineers  
- Systems Engineers  
- Test & Verification Engineers  
- Technical Program Managers  
- New Joiners & Interns  

---

## 🗂️ Wiki Structure

### 1️⃣ Engineering Processes
- Project lifecycle overview
- Requirement flow-down (System → Subsystem → Item)
- DAL / criticality assignment
- Design reviews (SRR, PDR, CDR, TRR, FRR)
- Change management & configuration control

📂 `/processes`

---

### 2️⃣ Requirements & Systems Engineering
- Requirement writing guidelines
- Traceability strategy
- ICD creation & ownership
- Fault tree analysis (FTA)
- Safety & hazard analysis

📂 `/systems-engineering`

---

### 3️⃣ Avionics Software
- Software architecture guidelines
- RTOS usage & scheduling strategy
- Coding standards (C / C++)
- Static analysis & unit testing
- Build, CI/CD, and artifact management
- DO-178C aligned practices (where applicable)

📂 `/avionics-software`

---

### 4️⃣ Avionics Hardware
- Board architecture guidelines
- Component selection philosophy
- Power, clocking, reset strategies
- EMI/EMC considerations
- Schematics, layout, and reviews
- Manufacturing & bring-up checklist

📂 `/avionics-hardware`

---

### 5️⃣ GNC Interfaces
- Avionics ↔ GNC data contracts
- Sensor models & assumptions
- Control loop timing & latency budgets
- Failure modes & degraded operation
- Simulation & HIL integration

📂 `/gnc-interfaces`

---

### 6️⃣ Communication Protocols
- UART / CAN / RS-485 / Ethernet usage
- Telemetry & telecommand formats
- Packet structures & timing constraints
- Error detection & recovery strategies

📂 `/communications`

---

### 7️⃣ Testing & Verification
- Unit testing strategy
- SIL / PIL / HIL testing
- Environmental & stress testing
- Test documentation templates
- Coverage & traceability expectations

📂 `/testing`

---

### 8️⃣ Tools & Tool Qualification
- Approved toolchain
- IDEs, compilers, debuggers
- Static analysis & testing tools
- Simulation tools
- Tool qualification notes (when applicable)

📂 `/tools`

---

### 9️⃣ Templates & Checklists
- Requirement templates
- ICD templates
- Design document templates
- Review checklists
- Test plan & report templates

📂 `/templates`

---

### 🔟 Lessons Learned & Best Practices
- Past failures & root causes
- Design anti-patterns
- Field issues & mitigations
- Performance optimization notes

📂 `/lessons-learned`

---

## 🧑‍💻 Contribution Guidelines

- Keep content **technical, factual, and actionable**
- Avoid undocumented assumptions
- Diagrams > long paragraphs
- Reference standards where applicable
- Update pages when designs or processes change

**Every engineer is expected to contribute.**

---

## 🔄 Versioning & Ownership

- Each section has a designated **owner**
- Major changes require review
- Obsolete content must be archived, not deleted

---

## 📌 Quick Links

- [Engineering Processes](./processes/README.md)
- [Avionics Software Guidelines](./avionics-software/README.md)
- [Avionics Hardware Guidelines](./avionics-hardware/README.md)
- [GNC Interfaces](./gnc-interfaces/README.md)
- [Templates](./templates/README.md)

---

## 🛠️ How to Use This Wiki

- **Before starting a task** → Check here
- **Before making an assumption** → Check here
- **After learning something painful** → Document it here

This wiki is a living system. Treat it like flight software.
