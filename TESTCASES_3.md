# API Test Cases Documentation - Part 2

## Test Cases for Seller, Statistics, and Delete Operations

Base URL: `https://qa-internship.avito.com/api/1`

---

## GET /:sellerID/item - Seller Items Tests

### TC_API_SELL_01: Get seller's items
- **Title:** Get seller's items
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/4359/item`
- **Request Body:** None
- **Expected Result:** `200 OK` - Array of seller's items returned
- **Actual Result:** `200 OK` - Multiple items returned with seller ID 4359
- **Status:** ✅ Passed

---

### TC_API_SELL_02: Empty seller
- **Title:** Get seller's items when seller has no items
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/6608/item`
- **Request Body:** None
- **Expected Result:** `200 OK` - Empty array returned
- **Actual Result:** `200 OK` - Empty array `[]`
- **Status:** ✅ Passed

---

### TC_API_SELL_03: Non-existent sellerID
- **Title:** Get items for non-existent seller
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/9988112341/item`
- **Request Body:** None
- **Expected Result:** `400 Bad Request` or `404 Not Found` - Seller not found
- **Actual Result:** `200 OK` - Empty array returned
- **Status:** ⚠️ Failed - Should validate seller exists

---

### TC_API_SELL_04: Negative sellerID
- **Title:** Get items with negative seller ID
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/-121/item`
- **Request Body:** None
- **Expected Result:** `400 Bad Request` - Invalid seller ID
- **Actual Result:** `200 OK` - Empty array returned
- **Status:** ⚠️ Failed - Should reject negative IDs

---

### TC_API_SELL_05: Zero sellerID
- **Title:** Get items with zero seller ID
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/0/item`
- **Request Body:** None
- **Expected Result:** `400 Bad Request` - Invalid seller ID
- **Actual Result:** `200 OK` - Empty array returned
- **Status:** ⚠️ Failed - Should reject zero ID

---

### TC_API_SELL_06: String sellerID
- **Title:** Get items with string seller ID
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/absdef/item`
- **Request Body:** None
- **Expected Result:** `400 Bad Request` - Invalid seller ID format
- **Actual Result:** `400 Bad Request` - Message: "передан некорректный идентификатор продавца"
- **Status:** ✅ Passed

---

### TC_API_SELL_07: Empty sellerID
- **Title:** Get items with empty seller ID in URL
- **Method & URL:** `GET https://qa-internship.avito.com/api/1//item`
- **Request Body:** None
- **Expected Result:** `404 Not Found` or `400 Bad Request`
- **Actual Result:** `405 Method Not Allowed`
- **Status:** ⚠️ Failed - Unexpected error code

---

### TC_API_SELL_08: No Authorization header
- **Title:** Request without bearer token
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/4359/item`
- **Request Body:** None
- **Authorization:** None
- **Expected Result:** `401 Unauthorized` - Valid bearer token required
- **Actual Result:** `401 Unauthorized` - Message: "valid bearer token is required"
- **Status:** ✅ Passed

---

### TC_API_SELL_09: Invalid token
- **Title:** Request with invalid/expired bearer token
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/4359/item`
- **Request Body:** None
- **Authorization:** Invalid Token
- **Expected Result:** `401 Unauthorized` - Invalid token
- **Actual Result:** `401 Unauthorized` - Message: "valid bearer token is required"
- **Status:** ✅ Passed

---

### TC_API_SELL_10: Another user's sellerID
- **Title:** Get items for different seller with valid auth
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/6608/item`
- **Request Body:** None
- **Authorization:** Token for user A (seller ID 4359)
- **Expected Result:** `403 Forbidden` - Unauthorized access to other seller's items
- **Actual Result:** `200 OK` - Items from seller 6608 returned
- **Status:** ⚠️ Failed - Should restrict cross-user access

---

## GET /statistic/:itemID - Statistics V1 Tests

### TC_API_STAT_V1_01: Existing item statistics
- **Title:** Get statistics for existing item
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/statistic/637ea861-f4da-473c-976a-148e2bb2f41d`
- **Request Body:** None
- **Expected Result:** `200 OK` - Statistics object returned
- **Actual Result:** `200 OK` - Statistics: { likes: 5, viewCount: 5, contacts: 5 }
- **Status:** ✅ Passed

---

### TC_API_STAT_V1_02: Verify likes, viewCount, contacts
- **Title:** Verify all statistics fields are returned correctly
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/statistic/856ba074-c9cb-420c-83f2-566105991a04`
- **Request Body:** None
- **Expected Result:** Statistics match: { likes: 21, viewCount: 11, contacts: 43 }
- **Actual Result:** { likes: 21, viewCount: 11, contacts: 43 } ✅ Matches
- **Status:** ✅ Passed

---

### TC_API_STAT_V1_03: Statistics consistency
- **Title:** Verify statistics don't change on repeated requests
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/statistic/856ba074-c9cb-420c-83f2-566105991a04`
- **Request Body:** None
- **Expected Result:** Same statistics returned on all requests
- **Actual Result:** Nothing changes in 4-5 requests (consistent)
- **Status:** ✅ Passed

---

### TC_API_STAT_V1_04: Large statistics
- **Title:** Get statistics with very large numbers
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/statistic/7040b980-3fd7-4256-945e-85c582b6e287`
- **Request Body:** None
- **Expected Result:** `200 OK` - Large numbers handled correctly
- **Actual Result:** `200 OK` - { likes: 999999999999999, viewCount: 999999999999999, contacts: 999999999999999 }
- **Status:** ✅ Passed

---

### TC_API_STAT_V1_05: Negative statistics
- **Title:** Get statistics with negative values
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/statistic/cc5a22d2-09f0-4a40-8bcb-9253e311f918`
- **Request Body:** None
- **Expected Result:** `200 OK` or `400 Bad Request` if validation exists
- **Actual Result:** `200 OK` - { likes: -21, viewCount: -431, contacts: -11 }
- **Status:** ⚠️ Failed - Negative values should not be stored

---

### TC_API_STAT_V1_06: Non-existent UUID
- **Title:** Get statistics for non-existent item
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/statistic/550e8400-e29b-41d4-a716-446655440999`
- **Request Body:** None
- **Expected Result:** `404 Not Found` - Item not found
- **Actual Result:** `404 Not Found` - Message: "statistic 550e8400-e29b-41d4-a716-446655440999 not found"
- **Status:** ✅ Passed

---

### TC_API_STAT_V1_07: Invalid UUID format
- **Title:** Get statistics with invalid UUID
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/statistic/12345312`
- **Request Body:** None
- **Expected Result:** `400 Bad Request` - Invalid UUID format
- **Actual Result:** `400 Bad Request` - Message: "передан некорректный идентификатор объявления"
- **Status:** ✅ Passed

---

### TC_API_STAT_V1_08: Random string ID
- **Title:** Get statistics with random string ID
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/statistic/abcdef`
- **Request Body:** None
- **Expected Result:** `400 Bad Request` - Invalid ID format
- **Actual Result:** `400 Bad Request` - Message: "передан некорректный идентификатор объявления"
- **Status:** ✅ Passed

---

### TC_API_STAT_V1_09: Empty ID
- **Title:** Get statistics with empty ID
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/statistic/`
- **Request Body:** None
- **Expected Result:** `404 Not Found` - Route not found
- **Actual Result:** `404 Not Found` - Message: "route /api/1/statistic/ not found"
- **Status:** ✅ Passed

---

### TC_API_STAT_V1_10: No Authorization
- **Title:** Get statistics without bearer token
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/statistic/cc5a22d2-09f0-4a40-8bcb-9253e311f918`
- **Request Body:** None
- **Authorization:** None
- **Expected Result:** `401 Unauthorized` - Valid bearer token required
- **Actual Result:** `401 Unauthorized` - Message: "valid bearer token is required"
- **Status:** ✅ Passed

---

### TC_API_STAT_V1_11: Another user's item
- **Title:** Get statistics for another user's item
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/statistic/470b0c01-1bd6-4612-b053-5f2c5534ea42` (user_b's item)
- **Request Body:** None
- **Authorization:** Token from user_a
- **Expected Result:** `403 Forbidden` - Unauthorized access
- **Actual Result:** `200 OK` - Statistics returned
- **Status:** ⚠️ Failed - Should restrict cross-user access

---

## GET /statistic/:itemID - Statistics V2 Tests

### TC_API_STAT_V2_01: Existing item statistics (V2)
- **Title:** Get statistics for existing item via V2 API
- **Method & URL:** `GET https://qa-internship.avito.com/api/2/statistic/470b0c01-1bd6-4612-b053-5f2c5534ea42`
- **Request Body:** None
- **Expected Result:** `200 OK` - Statistics returned
- **Actual Result:** `200 OK` - { likes: 5, viewCount: 20, contacts: 2 }
- **Status:** ✅ Passed

---

### TC_API_STAT_V2_02: Verify statistics consistency
- **Title:** Verify statistics match between requests
- **Method & URL:** `GET https://qa-internship.avito.com/api/2/statistic/470b0c01-1bd6-4612-b053-5f2c5534ea42`
- **Request Body:** None
- **Expected Result:** Same statistics as stored
- **Actual Result:** { likes: 5, viewCount: 20, contacts: 2 } ✅ Matches
- **Status:** ✅ Passed

---

### TC_API_STAT_V2_03: V1 vs V2 consistency
- **Title:** Verify V1 and V2 API return same data
- **Method & URL:**
  - `GET https://qa-internship.avito.com/api/1/statistic/470b0c01-1bd6-4612-b053-5f2c5534ea42`
  - `GET https://qa-internship.avito.com/api/2/statistic/470b0c01-1bd6-4612-b053-5f2c5534ea42`
- **Request Body:** None
- **Expected Result:** Both versions return identical data
- **Actual Result:** { likes: 5, viewCount: 20, contacts: 2 } - Both return same data ✅
- **Status:** ✅ Passed

---

### TC_API_STAT_V2_04: Large statistics (V2)
- **Title:** Get large statistics via V2 API
- **Method & URL:** `GET https://qa-internship.avito.com/api/2/statistic/2d203141-2d3a-4a55-9491-ece095e1c33a`
- **Request Body:** None
- **Expected Result:** `200 OK` - Large numbers handled
- **Actual Result:** `200 OK` - { likes: 999999999999999, viewCount: 999999999999999, contacts: 999999999999999 }
- **Status:** ✅ Passed

---

### TC_API_STAT_V2_05: Non-existent UUID (V2)
- **Title:** Get statistics for non-existent item via V2
- **Method & URL:** `GET https://qa-internship.avito.com/api/2/statistic/550e8400-e29b-41d4-a716-446655440999`
- **Request Body:** None
- **Expected Result:** `404 Not Found`
- **Actual Result:** `404 Not Found` - Message: "statistic 550e8400-e29b-41d4-a716-446655440999 not found"
- **Status:** ✅ Passed

---

### TC_API_STAT_V2_06: Invalid UUID (V2)
- **Title:** Get statistics with invalid UUID via V2
- **Method & URL:** `GET https://qa-internship.avito.com/api/2/statistic/550e8400`
- **Request Body:** None
- **Expected Result:** `400 Bad Request` - Invalid UUID
- **Actual Result:** `400 Bad Request` - Message: "передан некорректный идентификатор объявления"
- **Status:** ✅ Passed

---

### TC_API_STAT_V2_07: No Authorization (V2)
- **Title:** Get statistics without token via V2
- **Method & URL:** `GET https://qa-internship.avito.com/api/2/statistic/470b0c01-1bd6-4612-b053-5f2c5534ea42`
- **Request Body:** None
- **Authorization:** None
- **Expected Result:** `401 Unauthorized`
- **Actual Result:** `401 Unauthorized` - Message: "valid bearer token is required"
- **Status:** ✅ Passed

---

### TC_API_STAT_V2_08: Another user's item (V2)
- **Title:** Get another user's item statistics via V2
- **Method & URL:** `GET https://qa-internship.avito.com/api/2/statistic/470b0c01-1bd6-4612-b053-5f2c5534ea42`
- **Request Body:** None
- **Authorization:** Different user's token
- **Expected Result:** `403 Forbidden` - Unauthorized access
- **Actual Result:** `200 OK` - Statistics returned
- **Status:** ⚠️ Failed - Should restrict cross-user access

---

## DELETE /item/:itemID - Item Deletion Tests

### TC_API_DEL_01: Normal deletion
- **Title:** Delete existing item successfully
- **Method & URL:** `DELETE https://qa-internship.avito.com/api/2/item/5ba30600-cdc1-4f8f-b149-e954c4b39e77`
- **Request Body:** None
- **Expected Result:** `200 OK` - Item deleted
- **Actual Result:** `200 OK`
- **Status:** ✅ Passed

---

### TC_API_DEL_02: Verify item after deletion
- **Title:** Verify deleted item cannot be retrieved
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/5ba30600-cdc1-4f8f-b149-e954c4b39e77`
- **Request Body:** None
- **Expected Result:** `404 Not Found` - Item deleted
- **Actual Result:** `404 Not Found` - Message: "item 5ba30600-cdc1-4f8f-b149-e954c4b39e77 not found"
- **Status:** ✅ Passed

---

### TC_API_DEL_03: Verify seller list after deletion
- **Title:** Verify deleted item removed from seller's list
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/4359/item`
- **Request Body:** None
- **Expected Result:** Deleted item not in list
- **Actual Result:** Item was not found in list - Confirmed removed
- **Status:** ✅ Passed

---

### TC_API_DEL_04: Verify statistics after deletion (route 1)
- **Title:** Verify statistics endpoint for deleted item
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/statistics/5ba30600-cdc1-4f8f-b149-e954c4b39e77`
- **Request Body:** None
- **Expected Result:** `404 Not Found` - Route doesn't exist (typo: statistics vs statistic)
- **Actual Result:** `404 Not Found` - Message: "route /api/1/statistics/... not found"
- **Status:** ✅ Passed

---

### TC_API_DEL_05: Verify statistics after deletion (route 2)
- **Title:** Verify statistics endpoint v2 for deleted item
- **Method & URL:** `GET https://qa-internship.avito.com/api/2/statistics/5ba30600-cdc1-4f8f-b149-e954c4b39e77`
- **Request Body:** None
- **Expected Result:** `404 Not Found` - Route doesn't exist
- **Actual Result:** `404 Not Found` - Message: "route /api/1/statistics/... not found"
- **Status:** ✅ Passed

---

### TC_API_DEL_06: Delete same item twice
- **Title:** Attempt to delete already deleted item
- **Method & URL:** `DELETE https://qa-internship.avito.com/api/2/item/5ba30600-cdc1-4f8f-b149-e954c4b39e77`
- **Request Body:** None
- **Expected Result:** `404 Not Found` - Item already deleted
- **Actual Result:** `500 Internal Server Error` - Empty message
- **Status:** ⚠️ Failed - Should return 404, not 500

---

### TC_API_DEL_07: Non-existent UUID deletion
- **Title:** Delete non-existent item
- **Method & URL:** `DELETE https://qa-internship.avito.com/api/2/item/550e8400-e29b-41d4-a716-446655440999`
- **Request Body:** None
- **Expected Result:** `404 Not Found` - Item not found
- **Actual Result:** `500 Internal Server Error` - Empty message
- **Status:** ⚠️ Failed - Should return 404, not 500

---

### TC_API_DEL_08: Invalid UUID deletion
- **Title:** Delete with invalid UUID format
- **Method & URL:** `DELETE https://qa-internship.avito.com/api/2/item/550e8400`
- **Request Body:** None
- **Expected Result:** `400 Bad Request` - Invalid UUID
- **Actual Result:** `400 Bad Request` - Message: "переданный id айтема некорректный"
- **Status:** ✅ Passed

---

### TC_API_DEL_09: Random string ID deletion
- **Title:** Delete with random string ID
- **Method & URL:** `DELETE https://qa-internship.avito.com/api/2/item/abcdef`
- **Request Body:** None
- **Expected Result:** `400 Bad Request` - Invalid ID format
- **Actual Result:** `400 Bad Request` - Message: "переданный id айтема некорректный"
- **Status:** ✅ Passed

---

### TC_API_DEL_10: Empty ID deletion
- **Title:** Delete with empty ID
- **Method & URL:** `DELETE https://qa-internship.avito.com/api/2/item/`
- **Request Body:** None
- **Expected Result:** `404 Not Found` - Route not found
- **Actual Result:** `404 Not Found` - Message: "route /api/2/item/ not found"
- **Status:** ✅ Passed

---

### TC_API_DEL_11: No Authorization
- **Title:** Delete without bearer token
- **Method & URL:** `DELETE https://qa-internship.avito.com/api/2/item/...`
- **Request Body:** None
- **Authorization:** None
- **Expected Result:** `401 Unauthorized` - Valid bearer token required
- **Actual Result:** `401 Unauthorized` - Message: "valid bearer token is required"
- **Status:** ✅ Passed

---

### TC_API_DEL_12: Another user's item deletion
- **Title:** Delete another user's item
- **Method & URL:** `DELETE https://qa-internship.avito.com/api/2/item/f3815fc0-0b5b-4e92-9960-291f6ac209ca` (user_b's item)
- **Request Body:** None
- **Authorization:** Token from user_a
- **Expected Result:** `403 Forbidden` - Cannot delete other user's item
- **Actual Result:** `200 OK` - Item deleted
- **Status:** ⚠️ Failed - Critical security issue: Can delete other users' items

---

### TC_API_DEL_13: Wrong HTTP method on DELETE endpoint
- **Title:** Test wrong HTTP methods on DELETE endpoint
- **Method & URL:** `POST, PUT, PATCH, GET https://qa-internship.avito.com/api/2/item/f3815fc0-0b5b-4e92-9960-291f6ac209ca`
- **Request Body:** None
- **Expected Result:** `405 Method Not Allowed` for all
- **Actual Result:**
  - POST: `405 Method Not Allowed`
  - PUT: `405 Method Not Allowed`
  - PATCH: `405 Method Not Allowed`
  - GET: `405 Method Not Allowed`
- **Status:** ✅ Passed

---

### TC_API_DEL_14: Delete UUID case sensitivity
- **Title:** Delete item with uppercase UUID
- **Method & URL:** `DELETE https://qa-internship.avito.com/api/2/item/55B4D06C-3B1C-4267-99B2-F84E4DFADDBB`
- **Request Body:** None
- **Expected Result:** `200 OK` - UUID case-insensitive
- **Actual Result:** `200 OK`
- **Status:** ✅ Passed

---

## Summary

**Total Test Cases:** 42

**Passed:** 31 ✅

**Failed:** 11 ⚠️

### Failed Tests Summary:

#### Security Issues (Critical):
1. **TC_API_SELL_10** - Can access another user's items without authorization
2. **TC_API_STAT_V1_11** - Can retrieve another user's statistics
3. **TC_API_STAT_V2_08** - Can retrieve another user's statistics (V2)
4. **TC_API_DEL_12** - ⚠️ CRITICAL: Can delete another user's items

#### Validation Issues:
5. **TC_API_SELL_03** - Non-existent seller returns empty array instead of error
6. **TC_API_SELL_04** - Negative seller ID returns empty array instead of error
7. **TC_API_SELL_05** - Zero seller ID returns empty array instead of error
8. **TC_API_SELL_07** - Empty seller ID returns 405 instead of 400/404
9. **TC_API_STAT_V1_05** - Negative statistics values not validated
10. **TC_API_DEL_06** - Double delete returns 500 instead of 404
11. **TC_API_DEL_07** - Non-existent item delete returns 500 instead of 404

### Recommendations:

#### Critical (Security):
- Implement proper authorization checks on DELETE endpoints
- Restrict seller items access to only the authenticated user's items
- Restrict statistics access to only the item owner

#### High Priority:
- Fix 500 errors on DELETE operations - return 404 for non-existent items
- Add validation for seller ID existence and valid ranges
- Add proper error handling for negative values

#### Medium Priority:
- Improve error messages for edge cases
- Standardize API responses across endpoints
- Add input validation for all endpoints
