# Agent-Native Department Specification (ANDS) v0.1

## Abstract

This document specifies a machine-executable model for an Agent-Native
Department (AND). It defines normative requirements for task definitions,
stateful execution, constraint enforcement, audit trace generation, and
delegation control.

Implementations claiming compliance with this specification MUST satisfy
all mandatory requirements defined in Section 4.

---

## Introduction

This specification defines how an Agent-Native Department (AND) executes
multi-step operational tasks using machine-executable semantics rather
than natural-language-only workflows.

The specification focuses on:

- Execution semantics
- Constraint enforcement
- Auditability
- Delegation control

This document does not define user interfaces, workflow design tools,
or vendor-specific deployment architectures.

Non-goals include:

- User interface or workflow design systems
- Natural-language-only task execution models
- Vendor-specific orchestration platforms
- Model architectures or training methods

This specification defines execution semantics only.

---

## Terminology

The key words "MUST", "MUST NOT", "SHOULD", "SHOULD NOT", and "MAY"
are to be interpreted as described in BCP 14 (RFC 2119, RFC 8174)
when, and only when, they appear in all capitals.

Agent  
: An execution principal that performs one or more task steps.

TaskDefinition  
: A machine-executable object that defines input schema, output schema,
  constraints, and execution plan.

ExecutionPlan  
: An ordered list of executable steps and transition rules.

ConstraintSet  
: A collection of policy and business constraints that gate execution.

ExecutionTrace  
: A step-level record of execution inputs, outputs, decisions, and
  state transitions.

DelegationRecord  
: A machine-readable record that authorizes one agent to act within a
  defined scope and validity period.

---

## Specification

### 4.1 Conformance

An implementation MAY claim "ANDS v0.1 Compliant" only if it satisfies all
requirements marked MUST or MUST NOT in this document.

An implementation that does not implement one or more SHOULD requirements
SHOULD disclose those deviations in its compatibility documentation.

Optional extensions MAY be added, but they MUST NOT weaken or bypass
requirements marked MUST or MUST NOT.

Conformance validation MUST be performed against `compliance/ands-compliance-definition-v0.1.md`.
Implementations MUST state the exact specification version and compliance
definition version used for validation in their declaration package.

The validation result MUST include:

- validation date (UTC, ISO 8601)
- validator type (`self` or `third_party`)
- profile evaluated (`core`, `audit`, `delegation`, or `full`)
- pass/fail result per mandatory requirement identifier
- deviation list for unimplemented SHOULD requirements

Self-declared compliance does not imply verified compliance.

---

### 4.2 TaskDefinition Object

A conforming implementation MUST represent each task as a `TaskDefinition`
object with at least the following fields:

- `task_id` (string)
- `input_schema` (JSON Schema)
- `output_schema` (JSON Schema)
- `constraints` (`ConstraintSet`)
- `execution_plan` (`ExecutionPlan`)
- `expected_output` (object or schema reference)

`task_id` MUST be unique within the issuer namespace.

`input_schema` and `output_schema` MUST be machine-parseable and versioned.

A task definition encoded only as free-form natural language MUST NOT be
considered conformant.

---

### 4.3 ExecutionPlan Object

`execution_plan` MUST contain an ordered `steps` array.

`steps` MUST contain at least 7 executable steps.

Each step MUST include:

- `step_id` (unique in plan scope)
- `action` (machine-executable operation identifier)
- `preconditions` (machine-verifiable predicates)
- `postconditions` (machine-verifiable predicates)

A conforming runtime MUST maintain state across all steps in a plan.

The runtime SHOULD support branching and retry semantics.

When branching or retry is implemented, resulting paths MUST be recorded in
`ExecutionTrace`.

---

### 4.4 ConstraintSet Object

`ConstraintSet` MUST include both:

- `policy_constraints`
- `business_constraints`

Before each step is executed, the runtime MUST evaluate relevant constraints.

If a required constraint check fails, the step MUST NOT execute.

The constraint layer MUST be non-bypassable by task authors, agents,
and client callers.

Implementations MAY include external regulatory constraints as additional
constraint categories.

---

### 4.5 ExecutionTrace Object

A conforming system MUST generate trace records for every step transition.

Each trace record MUST include:

- `trace_id`
- `task_id`
- `step_id`
- `agent_id`
- `timestamp`
- `input_ref` (or stable hash)
- `output_ref` (or stable hash)
- `constraint_decision`
- `execution_result`

Trace records MUST preserve ordering to reconstruct the full task chain.

The system MUST support deterministic replay of a task chain from retained
trace data and associated immutable inputs.

---

### 4.6 Agent Identity and Delegation

Each agent MUST have a unique `agent_id`.

A delegation operation MUST create a `DelegationRecord` containing:

- `delegator_agent_id`
- `delegatee_agent_id`
- `scope`
- `valid_from`
- `valid_until` (or explicit revocation-only policy)
- `revocation_status`

The runtime MUST verify active delegation scope before a delegatee performs
a delegated step.

The runtime MUST support revocation and MUST deny execution for revoked
or expired delegations.

---

### 4.7 Compatibility Declaration Package

A system claiming conformance MUST provide a compatibility declaration
package including:

- task schema definition
- example task chain
- audit log sample
- constraint configuration sample

The declaration SHOULD identify unsupported SHOULD requirements.

---

### 4.8 Prohibited Claims

An implementation MUST NOT claim conformance if any of the following is true:

- it lacks step-level audit capability
- it supports only natural-language workflows without machine-executable
  task definitions
- it allows constraint enforcement bypass for execution paths

---

### 4.9 Conformance Profiles

Implementations MAY declare conformance to specific profiles, such as:

- Core Profile (TaskDefinition, ExecutionPlan, ConstraintSet)
- Audit Profile (ExecutionTrace and replay capability)
- Delegation Profile (identity and delegation enforcement)

Profiles MUST explicitly list included and excluded capabilities.

Profiles MUST NOT claim full conformance unless all mandatory requirements
in Sections 4.2–4.6 are satisfied.

---

## Security Considerations

A conforming implementation MUST enforce integrity protections for constraint
checks and trace records.

Implementations MUST protect trace records against unauthorized modification
through tamper-evident storage, append-only logs, or equivalent integrity
controls.

Implementations MUST authenticate agents and authorize each step execution
against current delegation and scope.

Constraint evaluation and execution authorization SHOULD be isolated from
untrusted client input paths.

Implementations SHOULD apply replay protection for execution requests,
including request identifiers, monotonic sequencing, or equivalent controls.

Audit retention and access policies SHOULD be defined to allow replay and
investigation while limiting unauthorized data exposure.

---

## References

### Normative References

- [RFC2119] Bradner, S., "Key words for use in RFCs to Indicate Requirement
  Levels", BCP 14, RFC 2119.
- [RFC8174] Leiba, B., "Ambiguity of Uppercase vs Lowercase in RFC 2119 Key
  Words", BCP 14, RFC 8174.

### Informative References

- EU AI Act
- ISO/IEC 42001
- NIST AI Risk Management Framework
- W3C Verifiable Credentials
