# Agent-Native Department Specification (ANDS) v0.1

## Official Release Report

- Release Date: 2026-02-27
- Release Status: Public Release
- Specification Version: ANDS v0.1
- Specification File: `rfc/ANDS-v0.1.md`
- Maintained By: SLASHLIFE AI, UNIPESSOAL LDA

---

## 1. Release Purpose

This report formally releases ANDS v0.1 and defines the minimum conditions,
scope boundaries, and verification artifacts required for a compliance claim.
ANDS v0.1 specifies machine-executable task-chain behavior and does not define
UI systems, vendor packaging, or model training methods.

---

## 2. Normative Scope

ANDS v0.1 defines normative requirements for the following core objects and
behaviors:

- `TaskDefinition`
- `ExecutionPlan`
- `ConstraintSet`
- `ExecutionTrace`
- `Agent` identity and `DelegationRecord`

Implementers MUST interpret requirements through the normative keywords
`MUST/SHOULD/MAY`. Any workflow that is defined only in natural language and
is not machine-executable MUST NOT be treated as ANDS-conformant.

---

## 3. Compliance Claim Conditions

A system may claim:

> "ANDS v0.1 Compliant"

only when all of the following are satisfied:

1. All `MUST` and `MUST NOT` requirements in the specification are satisfied.
2. A Compatibility Declaration Package is provided, including at least:
   - Task schema definition
   - Example task chain
   - Audit log sample
   - Constraint configuration sample
3. None of the following conditions exist:
   - Missing step-level audit capability
   - Natural-language-only workflow support without machine-executable task
     definitions
   - Any path that bypasses constraint enforcement

If one or more `SHOULD` requirements are not implemented, deviations SHOULD be
disclosed explicitly in compatibility documentation.

---

## 4. Mandatory Technical Requirement Summary

### 4.1 Task and Execution

- Each `TaskDefinition` MUST include machine-parseable, versioned input and
  output schema.
- `ExecutionPlan.steps` MUST contain at least 7 executable steps.
- Runtime execution MUST maintain cross-step state.

### 4.2 Constraints

- `ConstraintSet` MUST include both policy constraints and business
  constraints.
- Relevant constraints MUST be evaluated before each step.
- Failed required constraint checks MUST block execution.
- The constraint layer MUST be non-bypassable.

### 4.3 Audit and Replay

- The system MUST produce step-level `ExecutionTrace` records.
- Trace records MUST preserve chain order for reconstruction.
- The system MUST support deterministic replay.

### 4.4 Identity and Delegation

- Each agent MUST have a unique identity.
- Delegation MUST include verifiable scope, validity, and revocation status.
- Revoked or expired delegation MUST be denied at execution time.

---

## 5. Security Release Statement

ANDS v0.1 requires conformant implementations to provide, at minimum:

- Integrity controls for constraint checks and trace records
- Tamper-evident protections for trace storage (for example, append-only or
  equivalent controls)
- Agent authentication and per-step authorization controls
- Replay protection controls
- Audit retention and access control policy

---

## 6. Reference and Interpretation Baseline

Normative:

- RFC 2119
- RFC 8174

Informative:

- EU AI Act
- ISO/IEC 42001
- NIST AI Risk Management Framework
- W3C Verifiable Credentials

---

## 7. Release Conclusion

ANDS v0.1 provides a publishable baseline with implementation-ready
requirements for Agent-Native Department systems. Compliance claims MUST be
supported by mandatory requirement conformance and declaration package
delivery, not by narrative statements without technical evidence.
