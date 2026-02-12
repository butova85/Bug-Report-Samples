# Bug Report Samples v1

## BR-001 — Invalid field in query returns generic error message
**Severity:** Medium  
**Priority:** P2

**Environment**
- Module: Feature layer query
- Role: Viewer
- Client: Browser

**Preconditions**
1. Layer is accessible.
2. Query UI/API is available.

**Steps**
1. Submit query using non-existing field name.
2. Execute request.

**Expected**
Validation message identifies invalid field name clearly.

**Actual**
Generic error returned without actionable detail.

**Impact**
Slower troubleshooting for QA/users; increases support time.

---

## BR-002 — Viewer role can access edit controls in UI
**Severity:** High  
**Priority:** P1

**Environment**
- Module: Feature layer editing UI
- Role: Viewer

**Preconditions**
1. Viewer account assigned.
2. Layer editing restricted to editors.

**Steps**
1. Login as Viewer.
2. Open layer details page.
3. Observe toolbar actions.

**Expected**
Edit actions hidden or disabled.

**Actual**
Edit controls appear enabled in UI (operation later fails).

**Impact**
Permission model appears inconsistent; confusing UX/security perception.

---

## BR-003 — Add feature allows over-length text in constrained field
**Severity:** High  
**Priority:** P1

**Environment**
- Module: Add feature
- Role: Editor

**Preconditions**
1. Field max length = 50.
2. Editing enabled.

**Steps**
1. Submit new feature with 120-char value in constrained field.
2. Save feature.

**Expected**
Validation blocks save and returns field-length message.

**Actual**
Request accepted; stored value truncated silently.

**Impact**
Potential data quality loss without user awareness.

---

## BR-004 — Delete response returns success for non-existing object ID
**Severity:** Medium  
**Priority:** P2

**Environment**
- Module: Delete operation
- Role: Editor

**Preconditions**
1. Non-existing object ID identified.

**Steps**
1. Execute delete for non-existing ID.
2. Review operation result.

**Expected**
Result indicates failure/not found.

**Actual**
Operation marked as success.

**Impact**
Audit trail and test verification become unreliable.

---

## BR-005 — Query with invalid geometry returns HTTP 200 with error payload
**Severity:** Medium  
**Priority:** P2

**Environment**
- Module: Spatial query
- Role: Viewer/Editor

**Preconditions**
1. Geometry query endpoint available.

**Steps**
1. Submit malformed geometry payload.
2. Inspect status code and body.

**Expected**
Client error status (4xx) with validation details.

**Actual**
HTTP 200 returned with embedded error object.

**Impact**
Client-side monitoring may misclassify failed requests as successful.

---

## BR-006 — Batch edit partial failure summary is unclear
**Severity:** Medium  
**Priority:** P2

**Environment**
- Module: Batch edit
- Role: Editor

**Preconditions**
1. Batch includes valid and invalid rows.

**Steps**
1. Submit mixed-validity batch edit.
2. Review response summary.

**Expected**
Per-row result clearly identifies failed records and reasons.

**Actual**
Summary lacks row-level clarity.

**Impact**
Hard to reconcile data corrections and retest efficiently.

---

## BR-007 — Repeated query occasionally returns inconsistent record count
**Severity:** High  
**Priority:** P1

**Environment**
- Module: Query endpoint
- Role: Viewer
- Condition: repeated runs

**Preconditions**
1. Static dataset (no edits during test window).

**Steps**
1. Run identical query 20 times.
2. Compare returned record counts.

**Expected**
Stable count across runs.

**Actual**
Intermittent count mismatch observed.

**Impact**
Trust in reporting and analytics is reduced.

---

## BR-008 — Attachment upload error lacks file-type guidance
**Severity:** Low  
**Priority:** P3

**Environment**
- Module: Attachments
- Role: Editor

**Preconditions**
1. File-type restrictions configured.

**Steps**
1. Upload unsupported file type.
2. Observe error message.

**Expected**
Error states unsupported type and accepted formats.

**Actual**
Generic “Upload failed” message only.

**Impact**
Poor UX; avoidable support requests.
