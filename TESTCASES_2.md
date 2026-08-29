# API Test Cases Documentation

## Test Cases for Item Management API

Base URL: `https://qa-internship.avito.com/api/1/item`

---

## POST /item - Item Creation Tests

### TC_API_ITEM_01: Normal item creation
- **Title:** Normal item creation
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_item_create_01",
  "price": 9900,
  "statistics": {
    "likes": 21,
    "viewCount": 11,
    "contacts": 43
  }
}
```
- **Expected Result:** `200 OK` with UUID in response
- **Actual Result:** `200 OK` - Item created with ID `12882f42-1f6c-44b3-9399-9e9498ad8e6f`
- **Status:** ✅ Passed

---

### TC_API_ITEM_02: Second item with unique data
- **Title:** Second item with unique data
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_item_create_02",
  "price": 15000,
  "statistics": {
    "likes": 5,
    "viewCount": 20,
    "contacts": 2
  }
}
```
- **Expected Result:** `200 OK` with unique UUID
- **Actual Result:** `200 OK` - Item created with ID `4c798e3a-df2f-432e-bb49-babfbcb2f2e6`
- **Status:** ✅ Passed

---

### TC_API_ITEM_03: Same name
- **Title:** Same name as existing item
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_item_create_01",
  "price": 20000,
  "statistics": {
    "likes": 10,
    "viewCount": 40,
    "contacts": 4
  }
}
```
- **Expected Result:** `200 OK` - Duplicate names are allowed
- **Actual Result:** `200 OK` - Item created with ID `c9055190-753d-4df2-9ae1-c0a508d9726c`
- **Status:** ✅ Passed

---

### TC_API_ITEM_04: Same price
- **Title:** Item with same price as existing
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_item_create_03",
  "price": 9900,
  "statistics": {
    "likes": 1,
    "viewCount": 20,
    "contacts": 1
  }
}
```
- **Expected Result:** `200 OK` - Duplicate prices are allowed
- **Actual Result:** `200 OK` - Item created with ID `75de6a70-f0bd-4edb-ba73-c36582b335c3`
- **Status:** ✅ Passed

---

### TC_API_ITEM_05: Same statistics
- **Title:** Item with identical statistics
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_item_create_04",
  "price": 3000,
  "statistics": {
    "likes": 21,
    "viewCount": 11,
    "contacts": 43
  }
}
```
- **Expected Result:** `200 OK` - System allows duplicate statistics
- **Actual Result:** `200 OK` - Item created with ID `f0d89402-98d8-4c46-a825-caf533a19b52`
- **Status:** ✅ Passed

---

### TC_API_ITEM_06: Minimum zero price
- **Title:** Item with zero price
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_zero_price",
  "price": 0,
  "statistics": {
    "likes": 0,
    "viewCount": 0,
    "contacts": 0
  }
}
```
- **Expected Result:** `400 Bad Request` - Price must be greater than 0
- **Actual Result:** `400 Bad Request` - Message: "поле price обязательно"
- **Status:** ✅ Passed

---

### TC_API_ITEM_07: Negative price
- **Title:** Item with negative price
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_negative_price",
  "price": -1,
  "statistics": {
    "likes": 0,
    "viewCount": 0,
    "contacts": 0
  }
}
```
- **Expected Result:** `400 Bad Request` - Negative price not allowed
- **Actual Result:** `400 Bad Request` - Message: "поле likes обязательно"
- **Status:** ⚠️ Failed - Wrong error message

---

### TC_API_ITEM_08: Large price
- **Title:** Item with extremely large price value
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_large_price",
  "price": 999999999999999999999,
  "statistics": {
    "likes": 1,
    "viewCount": 1,
    "contacts": 1
  }
}
```
- **Expected Result:** `400 Bad Request` - Price exceeds maximum value
- **Actual Result:** `400 Bad Request` - Message: "не передано тело объявления"
- **Status:** ⚠️ Failed - Invalid JSON parsing

---

### TC_API_ITEM_09: Empty name
- **Title:** Item with empty name
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "",
  "price": 1000,
  "statistics": {
    "likes": 1,
    "viewCount": 1,
    "contacts": 1
  }
}
```
- **Expected Result:** `400 Bad Request` - Name cannot be empty
- **Actual Result:** `400 Bad Request` - Message: "поле name обязательно"
- **Status:** ✅ Passed

---

### TC_API_ITEM_10: Null name
- **Title:** Item with null name
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": null,
  "price": 1000,
  "statistics": {
    "likes": 1,
    "viewCount": 1,
    "contacts": 1
  }
}
```
- **Expected Result:** `400 Bad Request` - Name is required
- **Actual Result:** `400 Bad Request` - Message: "поле name обязательно"
- **Status:** ✅ Passed

---

### TC_API_ITEM_11: Very long name
- **Title:** Item with very long name (255+ characters)
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "aaaa...aaaa (255+ characters)",
  "price": 1000,
  "statistics": {
    "likes": 1,
    "viewCount": 1,
    "contacts": 1
  }
}
```
- **Expected Result:** `200 OK` or `400 Bad Request` if length limit exists
- **Actual Result:** `200 OK` - Item created with ID `a41c9dfa-75af-4214-84ed-087e63412c5c`
- **Status:** ✅ Passed - No length restriction

---

### TC_API_ITEM_12: Name with spaces
- **Title:** Item name with leading/trailing spaces
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "    test     item     ",
  "price": 1000,
  "statistics": {
    "likes": 1,
    "viewCount": 1,
    "contacts": 1
  }
}
```
- **Expected Result:** `200 OK` - Spaces are preserved or trimmed
- **Actual Result:** `200 OK` - Item created with ID `fd9d768e-fa52-44ef-8d58-3869769589fd`
- **Status:** ✅ Passed

---

### TC_API_ITEM_13: Special characters in name
- **Title:** Item name with special characters
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "Test !@#$%^&*()",
  "price": 1000,
  "statistics": {
    "likes": 1,
    "viewCount": 1,
    "contacts": 1
  }
}
```
- **Expected Result:** `200 OK` - Special characters allowed
- **Actual Result:** `200 OK` - Item created with ID `2a2e1685-b0f4-4a1c-a5ad-8f58b0e13a9f`
- **Status:** ✅ Passed

---

### TC_API_ITEM_14: Cyrillic name
- **Title:** Item name in Russian (Cyrillic)
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "Тестовое объявление",
  "price": 1000,
  "statistics": {
    "likes": 1,
    "viewCount": 1,
    "contacts": 1
  }
}
```
- **Expected Result:** `200 OK` - Cyrillic characters supported
- **Actual Result:** `200 OK` - Item created with ID `5b93f272-b60e-43ed-b7de-48d098f2f169`
- **Status:** ✅ Passed

---

### TC_API_ITEM_15: Empty statistics object
- **Title:** Item with empty statistics object
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_empty_statistics",
  "price": 1000,
  "statistics": {}
}
```
- **Expected Result:** `400 Bad Request` - Statistics fields required
- **Actual Result:** `400 Bad Request` - Message: "поле likes обязательно"
- **Status:** ✅ Passed

---

### TC_API_ITEM_16: Null statistics
- **Title:** Item with null statistics
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_null_statistics",
  "price": 1000,
  "statistics": null
}
```
- **Expected Result:** `400 Bad Request` - Statistics object required
- **Actual Result:** `400 Bad Request` - Message: "поле likes обязательно"
- **Status:** ✅ Passed

---

### TC_API_ITEM_17: Missing statistics
- **Title:** Item without statistics field
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_missing_statistics",
  "price": 1000
}
```
- **Expected Result:** `400 Bad Request` - Statistics object required
- **Actual Result:** `400 Bad Request` - Message: "поле likes обязательно"
- **Status:** ✅ Passed

---

### TC_API_ITEM_18: Null statistics values
- **Title:** Statistics with all null values
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_null_stats_values",
  "price": 1000,
  "statistics": {
    "likes": null,
    "viewCount": null,
    "contacts": null
  }
}
```
- **Expected Result:** `400 Bad Request` - Statistics values required
- **Actual Result:** `400 Bad Request` - Message: "поле likes обязательно"
- **Status:** ✅ Passed

---

### TC_API_ITEM_19: Negative likes
- **Title:** Statistics with negative likes value
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_negative_likes",
  "price": 1000,
  "statistics": {
    "likes": -1,
    "viewCount": 1,
    "contacts": 1
  }
}
```
- **Expected Result:** `400 Bad Request` - Statistics values must be >= 0
- **Actual Result:** `200 OK` - Item created with ID `dbbd1bf2-ba5e-4205-8d35-284e588fcc23`
- **Status:** ⚠️ Failed - Should reject negative values

---

### TC_API_ITEM_20: Negative view count
- **Title:** Statistics with negative viewCount
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_negative_views",
  "price": 1000,
  "statistics": {
    "likes": 1,
    "viewCount": -1,
    "contacts": 1
  }
}
```
- **Expected Result:** `400 Bad Request` - Statistics values must be >= 0
- **Actual Result:** `200 OK` - Item created with ID `8ad25b32-7d5e-4246-895e-b05ffce1bebf`
- **Status:** ⚠️ Failed - Should reject negative values

---

### TC_API_ITEM_21: Negative contacts
- **Title:** Statistics with negative contacts
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_negative_contacts",
  "price": 1000,
  "statistics": {
    "likes": 1,
    "viewCount": 1,
    "contacts": -1
  }
}
```
- **Expected Result:** `400 Bad Request` - Statistics values must be >= 0
- **Actual Result:** `200 OK` - Item created with ID `9382f865-83bf-44d5-b84a-a6d115bc3959`
- **Status:** ⚠️ Failed - Should reject negative values

---

### TC_API_ITEM_22: Very large statistics
- **Title:** Statistics with very large numbers
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_large_statistics",
  "price": 1000,
  "statistics": {
    "likes": 999999999999999,
    "viewCount": 999999999999999,
    "contacts": 999999999999999
  }
}
```
- **Expected Result:** `200 OK` or `400 Bad Request` if limit exists
- **Actual Result:** `200 OK` - Item created with ID `ce2d3919-6245-4897-931b-e99b4e8de256`
- **Status:** ✅ Passed

---

### TC_API_ITEM_23: Missing seller ID
- **Title:** Request without sellerID
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "name": "qa_missing_seller",
  "price": 1000,
  "statistics": {
    "likes": 1,
    "viewCount": 1,
    "contacts": 1
  }
}
```
- **Expected Result:** `400 Bad Request` - sellerID is required
- **Actual Result:** `400 Bad Request` - Message: "поле sellerID обязательно"
- **Status:** ✅ Passed

---

### TC_API_ITEM_24: Null seller ID
- **Title:** Request with null sellerID
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": null,
  "name": "qa_null_seller",
  "price": 1000,
  "statistics": {
    "likes": 1,
    "viewCount": 1,
    "contacts": 1
  }
}
```
- **Expected Result:** `400 Bad Request` - sellerID is required
- **Actual Result:** `400 Bad Request` - Message: "поле sellerID обязательно"
- **Status:** ✅ Passed

---

### TC_API_ITEM_25: Non-existent sellerID
- **Title:** Request with non-existent seller
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 999999999,
  "name": "qa_nonexistent_seller",
  "price": 1000,
  "statistics": {
    "likes": 1,
    "viewCount": 1,
    "contacts": 1
  }
}
```
- **Expected Result:** `400 Bad Request` - Seller doesn't match authenticated user
- **Actual Result:** `400 Bad Request` - Message: "sellerID должен совпадать с идентификатором авторизованного пользователя"
- **Status:** ✅ Passed

---

### TC_API_ITEM_26: sellerID as string
- **Title:** sellerID provided as string instead of number
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": "4359",
  "name": "qa_string_seller",
  "price": 1000,
  "statistics": {
    "likes": 1,
    "viewCount": 1,
    "contacts": 1
  }
}
```
- **Expected Result:** `400 Bad Request` - sellerID must be number
- **Actual Result:** `400 Bad Request` - Message: "не передано тело объявления"
- **Status:** ✅ Passed

---

### TC_API_ITEM_27: sellerID as boolean
- **Title:** sellerID provided as boolean
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": true,
  "name": "qa_boolean_seller",
  "price": 1000,
  "statistics": {
    "likes": 1,
    "viewCount": 1,
    "contacts": 1
  }
}
```
- **Expected Result:** `400 Bad Request` - sellerID type mismatch
- **Actual Result:** `400 Bad Request` - Message: "не передано тело объявления"
- **Status:** ✅ Passed

---

### TC_API_ITEM_28: Empty JSON
- **Title:** Request with empty JSON object
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{}
```
- **Expected Result:** `400 Bad Request` - All required fields missing
- **Actual Result:** `400 Bad Request` - Message: "поле name обязательно"
- **Status:** ✅ Passed

---

### TC_API_ITEM_29: Only sellerID
- **Title:** Request with only sellerID field
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359
}
```
- **Expected Result:** `400 Bad Request` - Missing required fields
- **Actual Result:** `400 Bad Request` - Message: "поле name обязательно"
- **Status:** ✅ Passed

---

### TC_API_ITEM_30: Missing price
- **Title:** Request without price field
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_missing_price",
  "statistics": {
    "likes": 1,
    "viewCount": 1,
    "contacts": 1
  }
}
```
- **Expected Result:** `400 Bad Request` - Price is required
- **Actual Result:** `400 Bad Request` - Message: "поле price обязательно"
- **Status:** ✅ Passed

---

### TC_API_ITEM_31: Wrong type price
- **Title:** Price provided as string instead of number
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_string_price",
  "price": "1000",
  "statistics": {
    "likes": 1,
    "viewCount": 1,
    "contacts": 1
  }
}
```
- **Expected Result:** `400 Bad Request` - Price type mismatch
- **Actual Result:** `400 Bad Request` - Message: "не передано тело объявления"
- **Status:** ✅ Passed

---

### TC_API_ITEM_32: Wrong statistics type
- **Title:** Statistics provided as string instead of object
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_wrong_statistics",
  "price": 1000,
  "statistics": "test"
}
```
- **Expected Result:** `400 Bad Request` - Statistics type mismatch
- **Actual Result:** `400 Bad Request` - Message: "не передано тело объявления"
- **Status:** ✅ Passed

---

### TC_API_ITEM_33: Extra fields
- **Title:** Request with unexpected extra fields
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_extra_fields",
  "price": 1000,
  "statistics": {
    "likes": 1,
    "viewCount": 1,
    "contacts": 1
  },
  "extraField": "unexpected",
  "anotherField": 123
}
```
- **Expected Result:** `200 OK` - Extra fields ignored
- **Actual Result:** `200 OK` - Item created with ID `f2c07e21-2570-491b-aa60-21c53cf21335`
- **Status:** ✅ Passed

---

### TC_API_ITEM_34: Malformed JSON
- **Title:** Request with invalid JSON syntax
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_extra_fields",
  "price": 1000,
  "statistics": {
    "likes": 1,
    "viewCount": 1,
    "contacts": 1
  }
```
- **Expected Result:** `400 Bad Request` - Invalid JSON
- **Actual Result:** `400 Bad Request` - Message: "не передан объект - объявление"
- **Status:** ✅ Passed

---

### TC_API_ITEM_35: Duplicate request
- **Title:** Sending same request twice
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_duplicate_request",
  "price": 5000,
  "statistics": {
    "likes": 5,
    "viewCount": 5,
    "contacts": 5
  }
}
```
- **Expected Result:** `200 OK` - Each request creates new item
- **Actual Result:** Two different items created with unique UUIDs
  - `3ba6cd49-0b14-4770-986c-200a4740b70e`
  - `4b0899ec-d8c2-4f5d-b5b0-eaf25153ce36`
- **Status:** ✅ Passed - No duplicate prevention

---

### TC_API_ITEM_36: UUID Uniqueness
- **Title:** Verify UUID uniqueness across multiple requests
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:**
```json
{
  "sellerID": 4359,
  "name": "qa_uuid_test",
  "price": 5000,
  "statistics": {
    "likes": 5,
    "viewCount": 5,
    "contacts": 5
  }
}
```
- **Expected Result:** `200 OK` - All UUIDs unique (5 requests)
- **Actual Result:** 5 unique UUIDs generated:
  - `b015a522-b581-48d5-a087-0c9087c3ef37`
  - `62ed48eb-acd4-4e99-b195-c4a6b467d779`
  - `60fe51b0-f5ea-436f-96bf-7773e7bdf1bf`
  - `c1abcc4e-c8da-4b11-8051-e25b4db0ec4f`
  - `cb18c615-a28b-4be9-8b2f-152119405382`
- **Status:** ✅ Passed

---

### TC_API_ITEM_37: Content-Type validation
- **Title:** Request with wrong Content-Type header
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Headers:** `Content-Type: text/plain`
- **Request Body:** Valid JSON body
- **Expected Result:** `400 Bad Request` - Content-Type must be application/json
- **Actual Result:** `400 Bad Request` - Message: "invalid content type"
- **Status:** ✅ Passed

---

### TC_API_ITEM_38: Missing Content-Type header
- **Title:** Request without Content-Type header
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Headers:** None
- **Request Body:** Valid JSON body
- **Expected Result:** `400 Bad Request` or `200 OK` depending on default handling
- **Actual Result:** `200 OK` - Request accepted without explicit header
- **Status:** ✅ Passed

---

### TC_API_ITEM_39: Accept header test
- **Title:** Request with wrong Accept header
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Headers:** `Accept: text/plain`
- **Request Body:** Valid JSON body
- **Expected Result:** `200 OK` - Accept header doesn't affect POST processing
- **Actual Result:** `200 OK` - Item created with ID `f27ae22c-09bf-4b43-aaff-b78a8d259a05`
- **Status:** ✅ Passed

---

### TC_API_ITEM_40: Rapid successive requests
- **Title:** Multiple rapid requests for same item
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Request Body:** Valid JSON body (sent 10 times rapidly)
- **Expected Result:** `200 OK` - All requests processed successfully
- **Actual Result:** 10 successful responses with unique UUIDs generated
- **Status:** ✅ Passed - No rate limiting detected

---

## GET /item/:id - Item Retrieval Tests

### TC_API_ITEM_41: Existing item retrieval
- **Title:** Retrieve existing item by valid UUID
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/12882f42-1f6c-44b3-9399-9e9498ad8e6f`
- **Request Body:** None
- **Expected Result:** `200 OK` - Item data returned
- **Actual Result:**
```json
{
    "createdAt": "2026-08-29 15:28:30.323391 +0300 +0300",
    "id": "12882f42-1f6c-44b3-9399-9e9498ad8e6f",
    "name": "qa_item_create_01",
    "price": 9900,
    "sellerId": 4359,
    "statistics": {
        "contacts": 43,
        "likes": 21,
        "viewCount": 11
    }
}
```
- **Status:** ✅ Passed

---

### TC_API_ITEM_42: Another existing item
- **Title:** Retrieve another existing item
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/637ea861-f4da-473c-976a-148e2bb2f41d`
- **Request Body:** None
- **Expected Result:** `200 OK` - Item data returned
- **Actual Result:**
```json
{
    "createdAt": "2026-08-29 17:09:22.245274 +0300 +0300",
    "id": "637ea861-f4da-473c-976a-148e2bb2f41d",
    "name": "qa_uuid_05",
    "price": 5000,
    "sellerId": 4359,
    "statistics": {
        "contacts": 5,
        "likes": 5,
        "viewCount": 5
    }
}
```
- **Status:** ✅ Passed

---

### TC_API_ITEM_43: Verify item data consistency
- **Title:** Verify retrieved item matches request data
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/12882f42-1f6c-44b3-9399-9e9498ad8e6f`
- **Request Body:** None
- **Expected Result:** All fields match original POST request
- **Actual Result:** ✅ All fields match:
  - name: "qa_item_create_01"
  - price: 9900
  - sellerId: 4359
  - statistics: { likes: 21, viewCount: 11, contacts: 43 }
- **Status:** ✅ Passed

---

### TC_API_ITEM_44: Verify name field
- **Title:** Verify name field is returned correctly
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/12882f42-1f6c-44b3-9399-9e9498ad8e6f`
- **Request Body:** None
- **Expected Result:** `"name": "qa_item_create_01"`
- **Actual Result:** `"name": "qa_item_create_01"`
- **Status:** ✅ Passed

---

### TC_API_ITEM_45: Verify price field
- **Title:** Verify price field is returned correctly
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/12882f42-1f6c-44b3-9399-9e9498ad8e6f`
- **Request Body:** None
- **Expected Result:** `"price": 9900`
- **Actual Result:** `"price": 9900`
- **Status:** ✅ Passed

---

### TC_API_ITEM_46: Verify statistics object
- **Title:** Verify statistics are returned correctly
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/12882f42-1f6c-44b3-9399-9e9498ad8e6f`
- **Request Body:** None
- **Expected Result:**
```json
{
  "likes": 21,
  "viewCount": 11,
  "contacts": 43
}
```
- **Actual Result:**
```json
{
  "likes": 21,
  "viewCount": 11,
  "contacts": 43
}
```
- **Status:** ✅ Passed

---

### TC_API_ITEM_47: Invalid UUID format
- **Title:** Request with invalid UUID format
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/12882f42`
- **Request Body:** None
- **Expected Result:** `400 Bad Request` - Invalid UUID
- **Actual Result:** `400 Bad Request` - Message: "ID айтема не UUID: 12882f42"
- **Status:** ✅ Passed

---

### TC_API_ITEM_48: Non-existent UUID
- **Title:** Request for non-existent item
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/12882f42-1f6c-44b3-9399-9e9499ad8e6f`
- **Request Body:** None
- **Expected Result:** `404 Not Found` - Item not found
- **Actual Result:** `404 Not Found` - Message: "item 12882f42-1f6c-44b3-9399-9e9499ad8e6f not found"
- **Status:** ✅ Passed

---

### TC_API_ITEM_49: Empty ID in URL
- **Title:** Request with empty item ID
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/`
- **Request Body:** None
- **Expected Result:** `404 Not Found` - Route not found
- **Actual Result:** `404 Not Found` - Message: "route /api/1/item/ not found"
- **Status:** ✅ Passed

---

### TC_API_ITEM_50: Random string as ID
- **Title:** Request with random string as ID
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/abcdef`
- **Request Body:** None
- **Expected Result:** `400 Bad Request` - Invalid UUID format
- **Actual Result:** `400 Bad Request` - Message: "ID айтема не UUID: abcdef"
- **Status:** ✅ Passed

---

### TC_API_ITEM_51: Uppercase UUID
- **Title:** Request with uppercase UUID
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/12882F42-1F6C-44B3-9399-9E9498AD8E6F`
- **Request Body:** None
- **Expected Result:** `200 OK` - UUID case-insensitive
- **Actual Result:** `200 OK` - Item returned with lowercase UUID
- **Status:** ✅ Passed

---

### TC_API_ITEM_52: UUID with spaces
- **Title:** Request with spaces around UUID
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/   12882F42-1F6C-44B3-9399-9E9498AD8E6F `
- **Request Body:** None
- **Expected Result:** `400 Bad Request` - Invalid UUID format
- **Actual Result:** `400 Bad Request` - Message: "ID айтема не UUID:   12882F42-1F6C-44B3-9399-9E9498AD8E6F "
- **Status:** ✅ Passed

---

### TC_API_ITEM_53: No Authorization header
- **Title:** Request without authorization
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/12882F42-1F6C-44B3-9399-9E9498AD8E6F`
- **Request Body:** None
- **Authorization:** None
- **Expected Result:** `401 Unauthorized` - Valid bearer token required
- **Actual Result:** `401 Unauthorized` - Message: "valid bearer token is required"
- **Status:** ✅ Passed

---

### TC_API_ITEM_54: Repeated GET requests
- **Title:** Multiple GET requests for same item
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/12882F42-1F6C-44B3-9399-9E9498AD8E6F`
- **Request Body:** None
- **Expected Result:** `200 OK` - Idempotent, no changes
- **Actual Result:** Same item returned every time, data unchanged
- **Status:** ✅ Passed

---

### TC_API_ITEM_55: Wrong HTTP method for GET endpoint
- **Title:** Test wrong HTTP methods on GET endpoint
- **Method & URL:**
  - `POST https://qa-internship.avito.com/api/1/item/12882F42-1F6C-44B3-9399-9E9498AD8E6F`
  - `PUT https://qa-internship.avito.com/api/1/item/12882F42-1F6C-44B3-9399-9E9498AD8E6F`
  - `PATCH https://qa-internship.avito.com/api/1/item/12882F42-1F6C-44B3-9399-9E9498AD8E6F`
  - `DELETE https://qa-internship.avito.com/api/1/item/12882F42-1F6C-44B3-9399-9E9498AD8E6F`
- **Request Body:** None
- **Expected Result:** `405 Method Not Allowed` for all
- **Actual Result:**
  - POST: `405 Method Not Allowed`
  - PUT: `405 Method Not Allowed`
  - PATCH: `405 Method Not Allowed`
  - DELETE: `405 Method Not Allowed`
- **Status:** ✅ Passed

---

## Summary

**Total Test Cases:** 55

**Passed:** 48 ✅

**Failed:** 7 ⚠️

### Failed Tests Summary:
1. **TC_API_ITEM_07** - Negative price validation error message
2. **TC_API_ITEM_08** - Large price causes JSON parsing error
3. **TC_API_ITEM_19** - Negative likes not validated
4. **TC_API_ITEM_20** - Negative viewCount not validated
5. **TC_API_ITEM_21** - Negative contacts not validated

### Recommendations:
- Implement proper validation for negative statistics values
- Improve error messages for edge cases
- Add length validation for large numeric values
- Consider implementing stricter input validation
