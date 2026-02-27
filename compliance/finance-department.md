# Example: Finance Agent-Native Department

## Scope

Handles:

- Invoice generation
- Payment tracking
- Expense validation
- Cross-border transaction documentation

## Task Chain Example

### Task: Invoice Processing

**Input:**
- client information
- service description
- billing entity (EU / Taiwan)

**Constraints:**
- Must comply with VAT / cross-border tax rules
- Must include contract reference
- Must not classify as commission

**Steps:**
1. Validate client data
2. Generate invoice document
3. Apply tax rules
4. Record transaction
5. Send invoice

**Expected Output:**
- Valid invoice document
- Transaction log
- Audit trace

## Audit

Each step must produce:

- execution log
- decision trace
- validation result

## Failure Modes

- invalid tax classification
- missing contract reference
- cross-border rule violation
