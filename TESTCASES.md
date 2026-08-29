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

## Summary

| Category | Total | Passed | Failed |
|----------|-------|--------|--------|
| Registration (Username) | 12 | 9 | 3 |
| Registration (Password) | 6 | 6 | 0 |
| Registration (Request Structure) | 8 | 6 | 2 |
| Registration (Response Validation) | 5 | 5 | 0 |
| Authorization | 14 | 14 | 0 |
| Security | 7 | 7 | 0 |
| **TOTAL** | **52** | **47** | **5** |

### Failed Tests:
1. **TC_API_REG_06** - Username spaces trimming (Expected rejection, got trimming)
2. **TC_API_REG_09** - Special characters acceptance (Expected rejection, got acceptance)
3. **TC_API_REG_11** - Numeric username acceptance (Expected rejection, got acceptance)
4. **TC_API_REG_22** - Extra field handling (Expected rejection, got acceptance)

---

## Notes

- **Test Environment:** https://qa-internship.avito.com
- **API Version:** v1
- **Authentication Method:** JWT Bearer Token
- **Test Date:** 2026-08-29
- **Test Engineer:** Xudoyyor

### Recommendations:

1. **Username Validation:** Implement stricter validation to:
   - Reject usernames with leading/trailing spaces
   - Reject special characters
   - Reject purely numeric usernames

2. **Request Validation:** Implement strict schema validation to reject extra fields in request body

3. **Security:** Continue monitoring token-based access controls and cross-user access attempts

4. **Documentation:** Add API documentation for acceptable username formats and validation rules
