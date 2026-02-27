# ANDS Core Profile v0.1

## Status

This document defines the Core Profile for ANDS v0.1.
It is a normative profile specification for implementations that require a
minimal, machine-executable ANDS subset.

## 1. Purpose

The Core Profile specifies the minimum interoperable capability set for an
Agent-Native Department implementation.

This profile is intended to support baseline deployment and profile-scoped
conformance claims without requiring full ANDS conformance.

## 2. Scope

The Core Profile includes the following capability domains:

- Task definition (`TaskDefinition`)
- Multi-step execution (`ExecutionPlan`)
- Constraint enforcement (`ConstraintSet`)
- Step-level traceability (`ExecutionTrace`)

The Core Profile excludes delegation lifecycle requirements defined in
ANDS v0.1 Section 4.6.

## 3. Normative Requirements

### 3.1 Task Definition Requirements

A Core Profile implementation MUST represent each task as a machine-executable
object with structured input, structured output, constraints, and an execution
plan.

Task definitions encoded only as free-form natural language MUST NOT be treated
as conformant.

### 3.2 Execution Requirements

The execution plan MUST contain at least seven executable steps.

The runtime MUST preserve execution state across all steps in a task chain.

The runtime SHOULD support branching and retry semantics. If branching or retry
is implemented, resulting execution paths MUST be represented in trace output.

### 3.3 Constraint Requirements

The runtime MUST enforce both policy constraints and business constraints.

Required constraint checks MUST be evaluated before step execution.

If a required constraint check fails, the corresponding step MUST NOT execute.

The constraint layer MUST be non-bypassable by task authors, agents, and
external callers.

### 3.4 Trace Requirements

The system MUST generate step-level execution trace records.

Trace records MUST preserve sequence information sufficient to reconstruct the
executed task chain.

The system SHOULD provide deterministic replay capability based on retained
trace and immutable input references.

## 4. Core Profile Conformance

An implementation MAY claim "ANDS Core Profile v0.1" only if it satisfies all
requirements marked MUST or MUST NOT in this profile.

A Core Profile claim MUST include a declaration package containing:

- Task schema definition
- Example task chain
- Audit log sample
- Constraint configuration sample

If one or more SHOULD requirements are not implemented, those deviations SHOULD
be disclosed in the declaration package.

A Core Profile claim MUST NOT be represented as full "ANDS v0.1 Compliant"
unless all mandatory requirements in ANDS v0.1 Sections 4.2 through 4.6 are
satisfied.

## 5. Explicit Exclusions

The following capabilities are out of scope for this profile:

- Delegation lifecycle enforcement
- Agent identity delegation verification under ANDS v0.1 Section 4.6
- Cross-domain identity federation
- Multi-agent negotiation protocols

Implementations MAY support these capabilities, but such support is not
required for Core Profile conformance.

## 6. Security Considerations

Core Profile implementations MUST protect constraint decisions and trace records
from unauthorized modification.

Core Profile implementations SHOULD isolate authorization and constraint
evaluation from untrusted client input paths.

Core Profile implementations SHOULD define retention and access-control policy
for trace data used in replay and investigation.

## 7. References

### Normative

- ANDS v0.1 Specification (`rfc/ANDS-v0.1.md`)
- ANDS Compliance Definition v0.1 (`compliance/ands-compliance-definition-v0.1.md`)
- RFC 2119
- RFC 8174

### Informative

- EU AI Act
- ISO/IEC 42001
- NIST AI Risk Management Framework
- W3C Verifiable Credentials
