# CCS Validation Rules
## Version 0.1.1

This document defines the official validation rules for CCS files.  
A CCS file is considered **valid** if and only if it satisfies all the rules below.

---

## 1. Required Top-Level Fields

A valid CCS file MUST contain:

- `system_id` (string)
- `version` (string)
- `core` (object)
- `governance` (object)
- `layers` (list)
- `agents` (list)

Missing any of these fields invalidates the file.

---

## 2. Core Validation

`core` MUST contain:

- `purpose` (string, non‑empty)

---

## 3. Governance Validation

`governance.policies` MUST contain at least:

- `P1_COST`
- `P2_TIME`
- `P3_ETHICS`
- `P4_ROBUSTNESS`
- `P5_TRANSPARENCY`
- `P6_PRIVACY`
- `P7_SOVEREIGNTY`
- `P8_INNOVATION`

Each policy MUST be:

- a number, OR  
- a string representing a governance mode

---

## 4. Layers Validation

Each layer MUST contain:

- `id` (string)
- `name` (string)
- `description` (string)

There MUST be at least **one** layer.

---

## 5. Agents Validation

Each agent MUST contain:

- `id` (string)
- `role` (string)
- `capabilities` (list of strings, at least 1)
- `limits` (object)

Inside `limits`, each field MUST be:

- a number, OR  
- a boolean

---

## 6. Traceability Requirements

A valid CCS implementation MUST:

- assign a unique `Trace_ID` to each execution  
- log the agent, layer, and timestamp  
- preserve logs for auditability  

---

## 7. Version Compatibility

A CCS file MUST declare:

```
version: "0.1.1"
```

Future versions MUST remain backward compatible unless explicitly stated.

---

## 8. Failure Conditions

A CCS file is **invalid** if:

- any required field is missing  
- any list is empty where at least one element is required  
- any type does not match the grammar  
- governance policies are incomplete  
- indentation breaks YAML structure  

---

## 9. Minimal Valid CCS Example

```
system_id: "example"
version: "0.1.1"

core:
  purpose: "Example system"

governance:
  policies:
    P1_COST: 0.01
    P2_TIME: 500
    P3_ETHICS: "STRICT"
    P4_ROBUSTNESS: "FAIL_GRACEFULLY"
    P5_TRANSPARENCY: "TRACEABLE"
    P6_PRIVACY: "MASK"
    P7_SOVEREIGNTY: "HUMAN_OVERRIDE"
    P8_INNOVATION: "ALLOWED"

layers:
  - id: "L1"
    name: "Intention"
    description: "Human defines the task"

agents:
  - id: "agent1"
    role: "Example agent"
    capabilities:
      - "do something"
    limits:
      max_cost: 0.01
```
