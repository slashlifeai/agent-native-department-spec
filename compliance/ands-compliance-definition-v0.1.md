# ANDS Compliance Definition v0.1

## 1. Purpose

This document defines the conditions under which a system may claim:

> "Compliant with Agent-Native Department Specification (ANDS)"

---

## 2. Compliance Levels

### Level 1 — Structural Compliance

The system MUST:

- Implement machine-executable task definitions
- Define input, constraints, and expected output
- Support multi-step execution (≥ 7 steps)

---

### Level 2 — Execution Compliance

The system MUST:

- Maintain stateful execution
- Record execution traces at each step
- Support reproducibility of task chains

---

### Level 3 — Constraint Compliance

The system MUST:

- Enforce policy constraints
- Enforce business rules
- Prevent bypass of constraint layer

---

### Level 4 — Audit Compliance

The system MUST:

- Provide step-level audit logs
- Support traceability from input to output
- Retain execution history

---

### Level 5 — Identity & Delegation Compliance

The system MUST:

- Assign unique identity to each agent
- Record delegation relationships
- Support revocation of delegation

---

## 3. Compliance Claim Rules

A system may only claim ANDS compliance if:

- All Level 1–3 requirements are fully implemented
- Any missing Level 4–5 features are explicitly disclosed

---

## 4. Prohibited Claims

The following are NOT permitted:

- Claiming compliance without audit capability
- Claiming compliance with only natural-language workflows
- Claiming compliance while bypassing constraint enforcement

---

## 5. Compatibility Declaration

A system claiming compliance MUST provide:

- Task schema definition
- Example task chain
- Audit log sample
- Constraint configuration

---

## 6. Verification (Optional)

Third-party or self-declared verification MAY include:

- Task execution replay
- Constraint enforcement test
- Audit log inspection

---

## 7. Versioning

Compliance MUST reference a specific version:

Example:
> "ANDS v0.1 Compliant"

---

## 8. Authority

This specification is maintained by:

SLASHLIFE AI, UNIPESSOAL LDA  
Portuguese Republic (European Union)
