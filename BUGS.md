# BUG REPORTS


---

## BUG-REG-001 (TC_API_REG_06)
- Title: Leading/trailing spaces in username are trimmed instead of rejected
- Test Case: TC_API_REG_06
- Steps to reproduce:
  1. POST /api/1/register with body `{ "username": " qa_test_123 ", "password": "StrongPassword123!" }`
  2. Observe response
- Expected: 400 Bad Request with message `"username must not contain leading or trailing spaces"`
- Actual: 201 Created; response returned `{"id": 4366, "username": "qa_test_123"}` (spaces trimmed and user created)
- Severity: High (input validation)
- Suggested fix: Do not trim leading/trailing whitespace on username server-side; validate and reject inputs with leading/trailing spaces. Add unit tests for trimming/validation.

---

## BUG-REG-002 (TC_API_REG_09)
- Title: Special characters allowed in username (should be restricted)
- Test Case: TC_API_REG_09
- Steps to reproduce:
  1. POST /api/1/register with `{ "username": "qa!@#$%^&*()", "password": "StrongPassword123!" }`
  2. Observe response
- Expected: 400 Bad Request with message `"username can only contain alphanumeric characters, underscores, and hyphens"`
- Actual: 201 Created; user created with special characters in username
- Severity: High (validation / potential security and normalization issues)
- Suggested fix: Enforce allowed character set for usernames at validation layer; sanitize/normalize input and reject disallowed characters.

---

## BUG-REG-003 (TC_API_REG_11)
- Title: Numeric-only username accepted (should be rejected)
- Test Case: TC_API_REG_11
- Steps to reproduce:
  1. POST /api/1/register with `{ "username": "123456789", "password": "StrongPassword123!" }`
  2. Observe response
- Expected: 400 Bad Request with message `"username cannot be purely numeric"`
- Actual: 201 Created; numeric username accepted
- Severity: High (business rule violation)
- Suggested fix: Add validation to reject usernames that are purely numeric or clearly document allowed formats if numeric usernames are acceptable.

---

## BUG-REG-004 (TC_API_REG_22)
- Title: Extra fields in registration payload are ignored instead of rejected
- Test Case: TC_API_REG_22
- Steps to reproduce:
  1. POST /api/1/register with `{ "username":"qa_unique_129","password":"StrongPassword123!","extraField":"test" }`
  2. Observe response
- Expected: 400 Bad Request with message `"unexpected field: extraField"` (strict schema expected)
- Actual: 201 Created; extraField ignored and user created
- Severity: Medium (schema strictness)
- Suggested fix: Decide on policy (strict vs permissive). If strict, reject unexpected fields with clear error. If permissive, document behavior.

---

## BUG-ITEM-001 (TC_API_ITEM_07)
- Title: Negative price returns incorrect error message
- Test Case: TC_API_ITEM_07
- Steps to reproduce:
  1. POST /api/1/item with `"price": -1` and valid other fields
  2. Observe response
- Expected: 400 Bad Request with a message indicating price must be > 0
- Actual: 400 Bad Request but message: "поле likes обязательно" (incorrect/misleading)
- Severity: Medium (incorrect error reporting)
- Suggested fix: Fix validation error mapping so price validation triggers correct error. Add tests for negative numeric fields to ensure proper messages.

---

## BUG-ITEM-002 (TC_API_ITEM_08)
- Title: Extremely large price causes JSON/body parsing error
- Test Case: TC_API_ITEM_08
- Steps to reproduce:
  1. POST /api/1/item with very large numeric literal for price (e.g., 999999999999999999999)
  2. Observe response
- Expected: 400 Bad Request with clear message `"price exceeds maximum allowed value"` or similar
- Actual: 400 Bad Request with message: "не передано тело объявления" (body not passed / JSON parsing error)
- Severity: High (data handling and robustness)
- Suggested fix: Handle large numeric values gracefully: validate numeric ranges before parsing into compact types, return descriptive validation error. Consider using string parsing or BigInt handling with explicit range checks.

---

## BUG-ITEM-003 (TC_API_ITEM_19)
- Title: Negative `likes` accepted when it should be rejected
- Test Case: TC_API_ITEM_19
- Steps to reproduce:
  1. POST /api/1/item with `"statistics": { "likes": -1, "viewCount": 1, "contacts": 1 }`
  2. Observe response
- Expected: 400 Bad Request — statistics values must be >= 0
- Actual: 200 OK — item created with negative likes
- Severity: High (data integrity)
- Suggested fix: Enforce non-negative validation for statistics fields at API layer and DB constraints if possible.

---

## BUG-ITEM-004 (TC_API_ITEM_20)
- Title: Negative `viewCount` accepted when it should be rejected
- Test Case: TC_API_ITEM_20
- Steps to reproduce:
  1. POST /api/1/item with `"statistics": { "likes": 1, "viewCount": -1, "contacts": 1 }`
- Expected: 400 Bad Request
- Actual: 200 OK — item created
- Severity: High
- Suggested fix: Same as ITEM-003 (validate non-negative values)

---

## BUG-ITEM-005 (TC_API_ITEM_21)
- Title: Negative `contacts` accepted when it should be rejected
- Test Case: TC_API_ITEM_21
- Steps to reproduce:
  1. POST /api/1/item with `"statistics": { "likes": 1, "viewCount": 1, "contacts": -1 }`
- Expected: 400 Bad Request
- Actual: 200 OK — item created
- Severity: High
- Suggested fix: Same as ITEM-003 (validate non-negative values)

---

## BUG-SELL-001 (TC_API_SELL_03)
- Title: Non-existent sellerID returns empty array instead of error
- Test Case: TC_API_SELL_03
- Steps to reproduce:
  1. GET /api/1/9988112341/item
  2. Observe response
- Expected: 400 Bad Request or 404 Not Found
- Actual: 200 OK — empty array `[]`
- Severity: Medium (ambiguity in API behavior)
- Suggested fix: Validate seller existence and return 404 (or documented 200 with explicit note). Prefer explicit error for non-existent resource.

---

## BUG-SELL-002 (TC_API_SELL_04)
- Title: Negative sellerID accepted (returns empty array) instead of validation error
- Test Case: TC_API_SELL_04
- Steps to reproduce:
  1. GET /api/1/-121/item
- Expected: 400 Bad Request
- Actual: 200 OK — empty array
- Severity: Medium
- Suggested fix: Validate numeric range for seller IDs; reject negative/zero IDs with 400.

---

## BUG-SELL-003 (TC_API_SELL_05)
- Title: SellerID=0 treated as valid (returns empty array) instead of error
- Test Case: TC_API_SELL_05
- Steps to reproduce:
  1. GET /api/1/0/item
- Expected: 400 Bad Request
- Actual: 200 OK — empty array
- Severity: Medium
- Suggested fix: Treat 0 as invalid seller id and return 400.

---

## BUG-SELL-004 (TC_API_SELL_07)
- Title: Empty sellerID path returns 405 Method Not Allowed (unexpected)
- Test Case: TC_API_SELL_07
- Steps to reproduce:
  1. GET /api/1//item
- Expected: 404 Not Found or 400 Bad Request
- Actual: 405 Method Not Allowed
- Severity: Low to Medium
- Suggested fix: Ensure router returns consistent 404 for missing path segment and improve route validation.

---

## BUG-SELL-005 (TC_API_SELL_10)
- Title: Accessing another user's seller items not restricted
- Test Case: TC_API_SELL_10
- Steps to reproduce:
  1. Authenticate as user A (sellerID 4359)
  2. GET /api/1/6608/item (seller B)
- Expected: 403 Forbidden (or documented behavior restricting cross-user access)
- Actual: 200 OK — items for seller 6608 returned
- Severity: High (authorization/ACL issue)
- Suggested fix: Enforce authorization checks so users can only access permitted seller resources. Add tests and review middleware.

---

## BUG-STAT-001 (TC_API_STAT_V1_05)
- Title: Negative statistics are stored and returned
- Test Case: TC_API_STAT_V1_05
- Steps to reproduce:
  1. Ensure an item has negative statistics in DB or create one via API
  2. GET /api/1/statistic/{itemID}
- Expected: 400 Bad Request on creation or normalized non-negative stats; at minimum disallow negative persisted stats
- Actual: 200 OK — negative numbers returned
- Severity: High (data integrity)
- Suggested fix: Validate statistics on creation/update and add DB constraints to prevent negative values.

---

## BUG-STAT-002 (TC_API_STAT_V1_11 & TC_API_STAT_V2_08)
- Title: Cross-user access to statistics allowed (should be restricted)
- Test Cases: TC_API_STAT_V1_11, TC_API_STAT_V2_08
- Steps to reproduce:
  1. Authenticate as user A
  2. GET /api/1/statistic/{item_of_user_B} or /api/2/statistic/{item_of_user_B}
- Expected: 403 Forbidden (authorization required)
- Actual: 200 OK — statistics for other user's item returned
- Severity: Critical (security)
- Suggested fix: Implement proper authorization checks for statistic endpoints; ensure token's user/sub is matched against item ownership.

---

## BUG-DEL-001 (TC_API_DEL_06)
- Title: Deleting an already-deleted item returns 500 instead of 404
- Test Case: TC_API_DEL_06
- Steps to reproduce:
  1. DELETE /api/2/item/{id} (delete item)
  2. DELETE same /api/2/item/{id} again
- Expected: 404 Not Found on second delete
- Actual: 500 Internal Server Error with empty message
- Severity: High (error handling)
- Suggested fix: Handle not-found condition gracefully and return 404. Add idempotent deletion handling and meaningful error body.

---

## BUG-DEL-002 (TC_API_DEL_07)
- Title: Deleting non-existent item returns 500 instead of 404
- Test Case: TC_API_DEL_07
- Steps to reproduce:
  1. DELETE /api/2/item/550e8400-e29b-41d4-a716-446655440999 (non-existent)
- Expected: 404 Not Found
- Actual: 500 Internal Server Error with empty message
- Severity: High (error handling)
- Suggested fix: Return 404 for non-existent resources. Ensure delete handler checks existence before attempting DB operations.

---

## BUG-DEL-003 (TC_API_DEL_12)
- Title: Deleting another user's item is allowed
- Test Case: TC_API_DEL_12
- Steps to reproduce:
  1. Authenticate as user A
  2. DELETE /api/2/item/{item_of_user_B}
- Expected: 403 Forbidden
- Actual: 200 OK — item deleted
- Severity: Critical (security)
- Suggested fix: Enforce ownership checks on DELETE endpoints. Add authorization middleware and audits; recover deleted data if possible and add tests to prevent regression.

---



