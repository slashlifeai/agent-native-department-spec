# ANDS Verified Mark
# Minimum Certification Mechanism v0.1

## Status

This document defines a minimum certification mechanism for issuing the
`ANDS Verified` mark.

## 1. Purpose

The `ANDS Verified` mark provides a bounded verification outcome that can be
referenced in procurement, compliance declarations, and technical due diligence.

The mechanism is designed to be lightweight, evidence-based, and profile-aware.

## 2. Verification Scope Levels

The mark MUST specify one of the following scope levels:

- `ANDS Verified — Core v0.1`
- `ANDS Verified — Full v0.1`

`Core` scope applies to `ANDS Core Profile v0.1` requirements.

`Full` scope applies to full `ANDS v0.1` conformance requirements.

## 3. Mandatory Inputs

A verification submission MUST include:

- Compatibility declaration package
- Completed RTM (`procurement/ANDS-core-profile-rtm-v0.1.md` or equivalent)
- Evidence artifacts for each mandatory requirement
- Verification report with pass/fail results by requirement ID

Evidence MUST be timestamped and linked to the evaluated software version.

## 4. Issuance Criteria

The `ANDS Verified` mark MAY be issued only if all of the following are true:

- All mandatory (`MUST` / `MUST NOT`) requirements in declared scope are PASS
- No unresolved FAIL entries remain for mandatory requirements
- SHOULD deviations are disclosed
- Prohibited claim conditions are not present

A mark MUST NOT be issued based only on narrative statements without objective
evidence.

## 5. Mark Statement Format

Issued marks MUST include:

- Verification scope (`Core` or `Full`)
- Version (`v0.1`)
- Evaluated implementation identifier (system name and version)
- Verification date (UTC, ISO 8601)
- Validator type (`self` or `third_party`)
- Verification reference ID

Example statement:

`ANDS Verified — Core v0.1 | System: Acme AND Runtime 2.3.1 | Date: 2026-02-27T12:30:00Z | Validator: third_party | Ref: ANDS-VER-2026-0042`

## 6. Validity and Renewal

A mark SHOULD have a fixed validity period.

Recommended default validity period: 12 months.

A mark MUST be re-verified before renewal when:

- Major runtime or policy-engine changes occur
- Constraint model changes materially
- Trace pipeline changes materially
- Previous nonconformities were remediated

## 7. Suspension and Revocation

A mark MUST be suspended or revoked if:

- Material evidence is found to be inaccurate
- Mandatory controls are later shown to be nonfunctional
- Constraint bypass is demonstrated in production-relevant conditions
- Submitted implementation version no longer matches deployed version

Revocation events MUST be documented with reason, date, and affected scope.

## 8. Procurement Usage

Procurement documents MAY require `ANDS Verified` as a pre-award or
post-award condition.

If required, procurement text MUST specify:

- Required scope (`Core` or `Full`)
- Minimum evidence package
- Acceptance authority
- Validity window at submission time

## 9. Relationship to Conformance Claims

`ANDS Verified` indicates that a defined scope has been evaluated against
objective evidence.

`ANDS Verified — Core v0.1` MUST NOT be represented as full
`ANDS v0.1 Compliant`.

`ANDS Verified` status does not replace legal, regulatory, or contractual
obligations outside the declared scope.

## 10. References

- `rfc/ANDS-v0.1.md`
- `profiles/core-profile-v0.1.md`
- `compliance/ands-compliance-definition-v0.1.md`
- `procurement/ANDS-minimum-procurement-spec-v0.1.md`
- `procurement/ANDS-core-profile-rtm-v0.1.md`
