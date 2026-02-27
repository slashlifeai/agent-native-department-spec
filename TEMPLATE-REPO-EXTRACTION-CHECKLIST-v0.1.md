# ANDS Template Repo Extraction Checklist v0.1

## Goal

Extract reusable RFC/profile/procurement/verification templates into a separate
repository, while keeping this repository as the authoritative ANDS content repo.

## 1. What to Move to `ands-rfc-template`

Move only reusable structure, wording patterns, and validation rules:

- RFC section skeleton:
  - `Abstract`
  - `Introduction`
  - `Terminology`
  - `Specification`
  - `Security Considerations`
  - `References`
- Profile document skeleton:
  - `Status`, `Purpose`, `Scope`, `Normative Requirements`, `Conformance`,
    `Exclusions`, `Security`, `References`
- Procurement spec skeleton:
  - conformance target, evidence package, claim restrictions, version pinning
- RTM skeleton:
  - requirement ID, source clause, evidence, verification method, status
- `ANDS Verified` mechanism skeleton:
  - scope, issuance criteria, mark statement format, revocation rules
- Writing conventions:
  - BCP14 keywords (`MUST/SHOULD/MAY`)
  - normative vs informative references
  - version string format

## 2. What Must Stay in This Repo

Keep all ANDS-specific authoritative content here:

- `rfc/ANDS-v0.1.md`
- `profiles/core-profile-v0.1.md`
- `procurement/ANDS-minimum-procurement-spec-v0.1.md`
- `procurement/ANDS-core-profile-rtm-v0.1.md`
- `verification/ANDS-verified-minimum-certification-v0.1.md`
- `compliance/ands-compliance-definition-v0.1.md`
- versioned release outputs and future amendment history

## 3. New Template Repo Baseline Structure

Suggested structure:

- `templates/rfc-template.md`
- `templates/profile-template.md`
- `templates/procurement-template.md`
- `templates/rtm-template.md`
- `templates/verified-mark-template.md`
- `guides/writing-rules.md`
- `guides/versioning-and-claims.md`
- `examples/` (generic, non-ANDS-specific examples)
- `checks/` (lint/validation rules)

## 4. Migration Steps (Order)

1. Create new repository `ands-rfc-template`.
2. Copy only generic template structures (no ANDS-specific claims text).
3. Add a template README with usage and versioning.
4. Add a changelog for template versions (for example, `v0.1.0`).
5. Tag the template repo release.
6. In this repo, add references to pinned template version.
7. Keep all normative ANDS decisions and claim semantics in this repo only.

## 5. Acceptance Criteria

Extraction is complete when all are true:

- Templates can generate equivalent document structure without ANDS-specific text.
- This repo still contains the normative source-of-truth content.
- Procurement and verification docs in this repo do not depend on floating template versions.
- Template repo is versioned and tagged independently.
- Cross-repo links pin explicit versions.

## 6. Risk Controls

- Do not move requirement IDs or normative obligations out of this repo.
- Do not let template repo redefine compliance semantics.
- Do not allow unpinned template references in procurement documents.
