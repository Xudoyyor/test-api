# API Test Cases Documentation

## Overview
This document contains comprehensive test cases for the Registration, Authorization, and Security endpoints of the Avito QA Internship API.

---

## 1. Registration Tests (Username Check)

### TC_API_REG_01: Normal registration
- **Test Case ID:** TC_API_REG_01
- **Title:** Normal registration
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_test_Xudoyyor",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `201 Created`
  - Response should contain `id` (number) and `username` (matching request)
- **Actual Result:** 
  ```json
  {
    "id": 4359,
    "username": "qa_test_Xudoyyor"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_02: Another unique user
- **Test Case ID:** TC_API_REG_02
- **Title:** Another unique user
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_test_Tycoon",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `201 Created`
  - Response should contain `id` (number) and `username` (matching request)
- **Actual Result:** 
  ```json
  {
    "id": 4360,
    "username": "qa_test_Tycoon"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_03: Empty username
- **Test Case ID:** TC_API_REG_03
- **Title:** Empty username
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"invalid JSON body"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid JSON body"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_04: Null username
- **Test Case ID:** TC_API_REG_04
- **Title:** Null username
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": null,
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"invalid JSON body"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid JSON body"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_05: Username only spaces
- **Test Case ID:** TC_API_REG_05
- **Title:** Username only spaces
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "        ",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"username must contain from 3 to 64 characters"`
- **Actual Result:** 
  ```json
  {
    "error": "username must contain from 3 to 64 characters"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_06: Username has spaces at the beginning and end
- **Test Case ID:** TC_API_REG_06
- **Title:** Username has spaces at the beginning and end
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": " qa_test_123 ",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"username must not contain leading or trailing spaces"`
- **Actual Result:** 
  ```json
  {
    "id": 4366,
    "username": "qa_test_123"
  }
  ```
- **Status:** ❌ Failed (Spaces were trimmed instead of rejected)

---

### TC_API_REG_07: Very short username
- **Test Case ID:** TC_API_REG_07
- **Title:** Very short username
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "a",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"username must contain from 3 to 64 characters"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid JSON body"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_08: Very long username
- **Test Case ID:** TC_API_REG_08
- **Title:** Very long username
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "aaaaa...(255 characters)",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"username must contain from 3 to 64 characters"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid JSON body"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_09: Special characters
- **Test Case ID:** TC_API_REG_09
- **Title:** Special characters
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa!@#$%^&*()",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"username can only contain alphanumeric characters, underscores, and hyphens"`
- **Actual Result:** 
  ```json
  {
    "id": 4368,
    "username": "qa!@#$%^&*()"
  }
  ```
- **Status:** ❌ Failed (Special characters were accepted)

---

### TC_API_REG_10: Cyrillic username
- **Test Case ID:** TC_API_REG_10
- **Title:** Cyrillic username
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "тестовый_пользователь",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `201 Created`
  - Response should contain `id` and `username`
- **Actual Result:** 
  ```json
  {
    "id": 4369,
    "username": "тестовый_пользователь"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_11: Numeric username
- **Test Case ID:** TC_API_REG_11
- **Title:** Numeric username
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "123456789",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"username cannot be purely numeric"`
- **Actual Result:** 
  ```json
  {
    "id": 4370,
    "username": "123456789"
  }
  ```
- **Status:** ❌ Failed (Numeric username was accepted)

---

### TC_API_REG_12: Duplicate username
- **Test Case ID:** TC_API_REG_12
- **Title:** Duplicate username
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_test_Tycoon",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `409 Conflict`
  - Error message: `"username is already registered"`
- **Actual Result:** 
  ```json
  {
    "error": "username is already registered"
  }
  ```
- **Status:** ✅ Passed

---

## 2. Password Tests

### TC_API_REG_13: Empty password
- **Test Case ID:** TC_API_REG_13
- **Title:** Empty password
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_test_unique_01",
    "password": ""
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"invalid JSON body"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid JSON body"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_14: Null password
- **Test Case ID:** TC_API_REG_14
- **Title:** Null password
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_test_unique_02",
    "password": null
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"invalid JSON body"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid JSON body"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_15: Very short password
- **Test Case ID:** TC_API_REG_15
- **Title:** Very short password
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_test_unique_03",
    "password": "a"
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"password must be at least 8 characters long"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid JSON body"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_16: Password with spaces
- **Test Case ID:** TC_API_REG_16
- **Title:** Password with spaces
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_test_unique_04",
    "password": " Strong Password 123 "
  }
  ```
- **Expected Result:** 
  - Status Code: `201 Created`
  - Response should contain `id` and `username`
- **Actual Result:** 
  ```json
  {
    "id": 4371,
    "username": "qa_test_unique_04"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_17: Very long password
- **Test Case ID:** TC_API_REG_17
- **Title:** Very long password
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_test_unique_05",
    "password": "aaaaa...(255 characters)"
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"password must not exceed 128 characters"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid JSON body"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_18: Password with special characters
- **Test Case ID:** TC_API_REG_18
- **Title:** Password with special characters
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_test_unique_06",
    "password": "!@#$%^&*()_+{}[]"
  }
  ```
- **Expected Result:** 
  - Status Code: `201 Created`
  - Response should contain `id` and `username`
- **Actual Result:** 
  ```json
  {
    "id": 4372,
    "username": "qa_test_unique_06"
  }
  ```
- **Status:** ✅ Passed

---

## 3. Request Structure Tests

### TC_API_REG_19: Empty JSON
- **Test Case ID:** TC_API_REG_19
- **Title:** Empty JSON
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {}
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"invalid JSON body"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid JSON body"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_20: Missing username
- **Test Case ID:** TC_API_REG_20
- **Title:** Missing username
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"invalid JSON body"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid JSON body"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_21: Missing password
- **Test Case ID:** TC_API_REG_21
- **Title:** Missing password
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_unique_128"
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"invalid JSON body"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid JSON body"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_22: Extra field
- **Test Case ID:** TC_API_REG_22
- **Title:** Extra field
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_unique_129",
    "password": "StrongPassword123!",
    "extraField": "test"
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"unexpected field: extraField"`
- **Actual Result:** 
  ```json
  {
    "id": 4407,
    "username": "qa_unique_129"
  }
  ```
- **Status:** ❌ Failed (Extra field was ignored instead of rejected)

---

### TC_API_REG_23: Username wrong data type
- **Test Case ID:** TC_API_REG_23
- **Title:** Username wrong data type
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": 123456,
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"invalid JSON body"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid JSON body"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_24: Password wrong data type
- **Test Case ID:** TC_API_REG_24
- **Title:** Password wrong data type
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_unique_130",
    "password": 123456
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"invalid JSON body"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid JSON body"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_25: Malformed JSON (missing closing brace)
- **Test Case ID:** TC_API_REG_25
- **Title:** Malformed JSON
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_unique_131",
    "password": "StrongPassword123!"
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"request body is required"` or JSON parse error
- **Actual Result:** 
  ```json
  {
    "message": "request body is required",
    "code": 400
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_26: Malformed JSON (duplicate)
- **Test Case ID:** TC_API_REG_26
- **Title:** Malformed JSON
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_unique_131",
    "password": "StrongPassword123!"
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"request body is required"` or JSON parse error
- **Actual Result:** 
  ```json
  {
    "message": "request body is required",
    "code": 400
  }
  ```
- **Status:** ✅ Passed

---

## 4. Response Validation Tests

### TC_API_REG_27: Is there an ID in the response?
- **Test Case ID:** TC_API_REG_27
- **Title:** ID in response
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_test_response_01",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Response contains `id` field
- **Actual Result:** 
  ```json
  {
    "id": 4359,
    "username": "qa_test_response_01"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_REG_28: ID data type
- **Test Case ID:** TC_API_REG_28
- **Title:** ID data type
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_test_response_02",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - `id` should be of type `Number` (integer)
- **Actual Result:** 
  - Type: `Number` ✓
- **Status:** ✅ Passed

---

### TC_API_REG_29: ID value
- **Test Case ID:** TC_API_REG_29
- **Title:** ID value
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_test_response_03",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - `id` should be a positive integer
- **Actual Result:** 
  - Value: `4359` (Positive) ✓
- **Status:** ✅ Passed

---

### TC_API_REG_30: Username in response
- **Test Case ID:** TC_API_REG_30
- **Title:** Username in response
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_test_response_04",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - `username` in response should match request: `"qa_test_response_04"`
- **Actual Result:** 
  - `"username": "qa_test_response_04"` ✓
- **Status:** ✅ Passed

---

### TC_API_REG_31: Password not in response
- **Test Case ID:** TC_API_REG_31
- **Title:** Password not in response
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/register`
- **Request Body:**
  ```json
  {
    "username": "qa_test_response_05",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Response should NOT contain `password` field
  - Response format: `{"id": 4359, "username": "qa_test_response_05"}`
- **Actual Result:** 
  ```json
  {
    "id": 4375,
    "username": "qa_test_response_05"
  }
  ```
- **Status:** ✅ Passed

---

## 5. Authorization Tests

### TC_API_AUTH_01: Normal authorization
- **Test Case ID:** TC_API_AUTH_01
- **Title:** Normal authorization
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/authorize`
- **Request Body:**
  ```json
  {
    "username": "qa_test_Xudoyyor",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `200 OK`
  - Response contains `accessToken` (JWT format) and `tokenType` = "Bearer"
- **Actual Result:** 
  ```json
  {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjQzNTksInVzZXJuYW1lIjoicWFfdGVzdF9YdWRveXlvciIsImV4cCI6MTc4ODA3OTcyMX0.fgLMFDhiSP5C-GF5Ouk_cPeD5Z9wRx-90rY7fdailMc",
    "tokenType": "Bearer"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_AUTH_02: Login after registration
- **Test Case ID:** TC_API_AUTH_02
- **Title:** Login after registration
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/authorize`
- **Request Body:**
  ```json
  {
    "username": "qa_test_Xudoyyor",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `200 OK`
  - Response contains `accessToken` and `tokenType`
- **Actual Result:** 
  ```json
  {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjQzNTksInVzZXJuYW1lIjoicWFfdGVzdF9YdWRveXlvciIsImV4cCI6MTc4ODA4MDExM30.4j3TN8A7EtiI12kkln_vtYkzhQlzENNB78R2E5NjEaU",
    "tokenType": "Bearer"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_AUTH_03: Repeated authorization
- **Test Case ID:** TC_API_AUTH_03
- **Title:** Repeated authorization
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/authorize`
- **Request Body:**
  ```json
  {
    "username": "qa_test_Xudoyyor",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `200 OK`
  - Each request generates a new token (tokens should differ)
- **Actual Result:** 
  - Token 1: `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjQzNTksInVzZXJuYW1lIjoicWFfdGVzdF9YdWRveXlvciIsImV4cCI6MTc4ODA4MDI4M30.VskVewGKqOlGq9WrXPRYDjLHclHN1WNZAt6atGWckCU`
  - Token 2: `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjQzNTksInVzZXJuYW1lIjoicWFfdGVzdF9YdWRveXlvciIsImV4cCI6MTc4ODA4MDI5NX0.yt9ZsiXFxl_rQwxqxChCjj_amrg9Im3PHchkho_gmKc`
  - Token 3: `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjQzNTksInVzZXJuYW1lIjoicWFfdGVzdF9YdWRveXlvciIsImV4cCI6MTc4ODA4MDMwOH0.l6pRkCvcfWakwffI4Lj3ejXay7ra8I-q8BMWVey0hss`
  - Token 4: `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjQzNTksInVzZXJuYW1lIjoicWFfdGVzdF9YdWRveXlvciIsImV4cCI6MTc4ODA4MDMxNn0.B3cye_6OiFhxTjWcqk2RprTldWwK3qZpJg3EUIpBfqs`
- **Status:** ✅ Passed

---

### TC_API_AUTH_04: Wrong password
- **Test Case ID:** TC_API_AUTH_04
- **Title:** Wrong password
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/authorize`
- **Request Body:**
  ```json
  {
    "username": "qa_test_Xudoyyor",
    "password": "WrongPassword999!"
  }
  ```
- **Expected Result:** 
  - Status Code: `401 Unauthorized`
  - Error message: `"invalid username or password"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid username or password"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_AUTH_05: Non-existent username
- **Test Case ID:** TC_API_AUTH_05
- **Title:** Non-existent username
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/authorize`
- **Request Body:**
  ```json
  {
    "username": "this_user_does_not_exist_987654",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `401 Unauthorized`
  - Error message: `"invalid username or password"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid username or password"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_AUTH_06: Empty username
- **Test Case ID:** TC_API_AUTH_06
- **Title:** Empty username
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/authorize`
- **Request Body:**
  ```json
  {
    "username": "",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"invalid JSON body"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid JSON body"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_AUTH_07: Empty password
- **Test Case ID:** TC_API_AUTH_07
- **Title:** Empty password
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/authorize`
- **Request Body:**
  ```json
  {
    "username": "qa_test_Xudoyyor",
    "password": ""
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"invalid JSON body"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid JSON body"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_AUTH_08: Missing username
- **Test Case ID:** TC_API_AUTH_08
- **Title:** Missing username
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/authorize`
- **Request Body:**
  ```json
  {
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"invalid JSON body"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid JSON body"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_AUTH_09: Missing password
- **Test Case ID:** TC_API_AUTH_09
- **Title:** Missing password
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/authorize`
- **Request Body:**
  ```json
  {
    "username": "qa_test_Xudoyyor"
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"invalid JSON body"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid JSON body"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_AUTH_10: Empty body
- **Test Case ID:** TC_API_AUTH_10
- **Title:** Empty body
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/authorize`
- **Request Body:**
  ```json
  {}
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"invalid JSON body"`
- **Actual Result:** 
  ```json
  {
    "error": "invalid JSON body"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_AUTH_11: Malformed JSON
- **Test Case ID:** TC_API_AUTH_11
- **Title:** Malformed JSON
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/authorize`
- **Request Body:**
  ```json
  {
    "username": "qa_test_Xudoyyor",
    "password": "StrongPassword123!"
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"request body is required"` or JSON parse error
- **Actual Result:** 
  ```json
  {
    "message": "request body is required",
    "code": 400
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_AUTH_12: Access token availability
- **Test Case ID:** TC_API_AUTH_12
- **Title:** Access token availability
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/authorize`
- **Request Body:**
  ```json
  {
    "username": "qa_test_Xudoyyor",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Status Code: `200 OK`
  - Response contains `accessToken` field with JWT value
- **Actual Result:** 
  ```json
  {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjQzNTksInVzZXJuYW1lIjoicWFfdGVzdF9YdWRveXlvciIsImV4cCI6MTc4ODA3OTcyMX0.fgLMFDhiSP5C-GF5Ouk_cPeD5Z9wRx-90rY7fdailMc",
    "tokenType": "Bearer"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_AUTH_13: Access token format
- **Test Case ID:** TC_API_AUTH_13
- **Title:** Access token format
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/authorize`
- **Request Body:**
  ```json
  {
    "username": "qa_test_Xudoyyor",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Token should be in JWT format (three parts separated by dots)
  - Token should contain user information (username, sub, exp)
- **Actual Result:** 
  - `"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjQzNTksInVzZXJuYW1lIjoicWFfdGVzdF9YdWRveXlvciIsImV4cCI6MTc4ODA3OTcyMX0.fgLMFDhiSP5C-GF5Ouk_cPeD5Z9wRx-90rY7fdailMc"`
  - Token format: Valid JWT ✓
- **Status:** ✅ Passed

---

### TC_API_AUTH_14: Password not in response
- **Test Case ID:** TC_API_AUTH_14
- **Title:** Password not in response
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/authorize`
- **Request Body:**
  ```json
  {
    "username": "qa_test_Xudoyyor",
    "password": "StrongPassword123!"
  }
  ```
- **Expected Result:** 
  - Response should NOT contain `password` field
  - Response format: `{"accessToken": "...", "tokenType": "Bearer"}`
- **Actual Result:** 
  ```json
  {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjQzNTksInVzZXJuYW1lIjoicWFfdGVzdF9YdWRveXlvciIsImV4cCI6MTc4ODA3OTcyMX0.fgLMFDhiSP5C-GF5Ouk_cPeD5Z9wRx-90rY7fdailMc",
    "tokenType": "Bearer"
  }
  ```
- **Status:** ✅ Passed

---

## 6. Security Tests

### TC_API_SEC_01: Protected endpoint without Authorization header
- **Test Case ID:** TC_API_SEC_01
- **Title:** Protected endpoint without Authorization header
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/68175190-d6b3-43a0-a974-fe845ad0284b`
- **Headers:** None
- **Expected Result:** 
  - Status Code: `401 Unauthorized`
  - Error message: `"valid bearer token is required"`
- **Actual Result:** 
  ```json
  {
    "error": "valid bearer token is required"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_SEC_02: Authorization header without Bearer prefix
- **Test Case ID:** TC_API_SEC_02
- **Title:** Authorization header without Bearer prefix
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/68175190-d6b3-43a0-a974-fe845ad0284b`
- **Headers:** 
  - `Authorization: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjQzNTksInVzZXJuYW1lIjoicWFfdGVzdF9YdWRveXlvciIsImV4cCI6MTc4ODA3OTcyMX0.fgLMFDhiSP5C-GF5Ouk_cPeD5Z9wRx-90rY7fdailMc`
- **Expected Result:** 
  - Status Code: `401 Unauthorized`
  - Error message: `"valid bearer token is required"`
- **Actual Result:** 
  ```json
  {
    "error": "valid bearer token is required"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_SEC_03: Empty bearer token
- **Test Case ID:** TC_API_SEC_03
- **Title:** Empty bearer token
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/68175190-d6b3-43a0-a974-fe845ad0284b`
- **Headers:** 
  - `Authorization: Bearer `
- **Expected Result:** 
  - Status Code: `401 Unauthorized`
  - Error message: `"valid bearer token is required"`
- **Actual Result:** 
  ```json
  {
    "error": "valid bearer token is required"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_SEC_04: Invalid token (tampered)
- **Test Case ID:** TC_API_SEC_04
- **Title:** Invalid token (tampered)
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/68175190-d6b3-43a0-a974-fe845ad0284b`
- **Headers:** 
  - `Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjQzNTksInVzZXJuYW1lIjoicWFfdGVzdF9YdWRveXlvciIsImV4cCI6MTc4ODA3OTcyMX0.fgLMFDhiSP5C-GF5Ouk_cPeD5Z9wRx-50rY7fdailMc`
- **Expected Result:** 
  - Status Code: `401 Unauthorized`
  - Error message: `"valid bearer token is required"`
- **Actual Result:** 
  ```json
  {
    "error": "valid bearer token is required"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_SEC_05: Malformed authorization header
- **Test Case ID:** TC_API_SEC_05
- **Title:** Malformed authorization header
- **Method & URL:** `GET https://qa-internship.avito.com/api/1/item/68175190-d6b3-43a0-a974-fe845ad0284b`
- **Headers:** 
  - `Authorization: BearerBearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjQzNTksInVzZXJuYW1lIjoicWFfdGVzdF9YdWRveXlvciIsImV4cCI6MTc4ODA3OTcyMX0.fgLMFDhiSP5C-GF5Ouk_cPeD5Z9wRx-90rY7fdailMc`
- **Expected Result:** 
  - Status Code: `401 Unauthorized`
  - Error message: `"valid bearer token is required"`
- **Actual Result:** 
  ```json
  {
    "error": "valid bearer token is required"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_SEC_06: User A token + User B sellerID
- **Test Case ID:** TC_API_SEC_06
- **Title:** User A token + User B sellerID
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Headers:** 
  - `Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjQzNjAsInVzZXJuYW1lIjoicWFfdGVzdF9UeWNvb24iLCJleHAiOjE3ODgwODUyMjF9.JOCMWpCS3B7kpteRAaxh28KpgZ8UkLlj2zdkEG8tzXc`
- **Request Body:**
  ```json
  {
    "sellerID": 4359,
    "name": "security_test_A_B",
    "price": 1000,
    "statistics": {
      "likes": 1,
      "viewCount": 1,
      "contacts": 1
    }
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"sellerID должен совпадать с идентификатором авторизованного пользователя"`
- **Actual Result:** 
  ```json
  {
    "result": {
      "message": "sellerID должен совпадать с идентификатором авторизованного пользователя",
      "messages": {}
    },
    "status": "400"
  }
  ```
- **Status:** ✅ Passed

---

### TC_API_SEC_07: Switching user via X-UserId header
- **Test Case ID:** TC_API_SEC_07
- **Title:** Switching user via X-UserId header
- **Method & URL:** `POST https://qa-internship.avito.com/api/1/item`
- **Headers:** 
  - `Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjQzNjAsInVzZXJuYW1lIjoicWFfdGVzdF9UeWNvb24iLCJleHAiOjE3ODgwODUyMjF9.JOCMWpCS3B7kpteRAaxh28KpgZ8UkLlj2zdkEG8tzXc`
  - `X-UserId: 4359`
- **Request Body:**
  ```json
  {
    "sellerID": 4359,
    "name": "x_user_test",
    "price": 1000,
    "statistics": {
      "likes": 1,
      "viewCount": 1,
      "contacts": 1
    }
  }
  ```
- **Expected Result:** 
  - Status Code: `400 Bad Request`
  - Error message: `"sellerID должен совпадать с идентификатором авторизованного пользователя"`
  - Verify that X-UserId header does NOT bypass user context
- **Actual Result:** 
  ```json
  {
    "result": {
      "message": "sellerID должен совпадать с идентификатором авторизованного пользователя",
      "messages": {}
    },
    "status": "400"
  }
  ```
- **Status:** ✅ Passed

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
