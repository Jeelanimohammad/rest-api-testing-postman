# Test Execution Summary Report

## 1. Project Overview
- **Project Name:** REST API Testing and Validation Using Postman
- **Target Application:** JSONPlaceholder Practice REST API (`https://jsonplaceholder.typicode.com`)
- **Domain Mapping:** Evaluated `/users` resource as student/member records (`Student Records API Testing`)
- **Execution Date:** October 2026
- **Test Environment:** Postman Free Edition (Desktop / Web Runner) & Automated HTTP Test Suite
- **Tester:** Mohammad Jeelani (QA Intern / Fresher)

---

## 2. Test Execution Statistics

| Metric | Count | Percentage |
| :--- | :--- | :--- |
| **Total Test Cases** | **24** | 100% |
| **Passed Tests** | **22** | 91.7% |
| **Failed Tests** | **2** | 8.3% |
| **Blocked Tests** | **0** | 0% |
| **Not Run** | **0** | 0% |
| **Defects Identified** | **3** | - |

---

## 3. Test Coverage by HTTP Method

| HTTP Method / Scenario | Test Count | Pass | Fail | Coverage Description |
| :--- | :--- | :--- | :--- | :--- |
| **GET Requests** | 9 | 9 | 0 | List retrieval, single record by ID, nested address/geo schema validation, query filters (`username`, `email`), response time checks |
| **POST Requests** | 3 | 3 | 0 | Single record creation, nested JSON structures (company, address), HTTP 201 status assertion |
| **PUT & PATCH Requests**| 3 | 3 | 0 | Full object replacement (PUT), partial attribute updates (PATCH) |
| **DELETE Requests** | 2 | 2 | 0 | Resource deletion simulation by ID, HTTP 200 validation |
| **Negative Testing** | 7 | 5 | 2 | Non-existent IDs (999), negative IDs (-1), alphanumeric IDs (`/users/abc`), invalid endpoint (`/invalid_students`), malformed JSON syntax (500 observed), empty payload schema bypass, invalid email regex format |

---

## 4. Key Assertions Implemented
Every request in the Postman collection contains beginner-friendly JavaScript test assertions validating:
1. **HTTP Status Code Verification**: Confirming expected codes (`200 OK`, `201 Created`, `404 Not Found`).
2. **Response Header & Format**: Validating `Content-Type` contains `application/json`.
3. **Response Time Benchmarking**: Ensuring API latency is under 1500ms.
4. **Data Type & Schema Verification**: Ensuring `id` is a number, `name` and `email` are strings, and nested structures exist.
5. **Payload Value Verification**: Confirming created or updated records echo the submitted fields accurately.

---

## 5. Identified Defects & Observations

| Bug ID | Endpoint | Method | Severity | Description | Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **BUG-API-01** | `/users` | POST | Medium | Missing schema validation: Empty JSON `{}` produces `201 Created` instead of expected `400 Bad Request`. | Open (Mock API Limitation) |
| **BUG-API-02** | `/users` | POST | Low | Missing data type/format validation: Sending `"email": "not-an-email-address"` succeeds with `201 Created` instead of `400 Bad Request`. | Open (Mock API Limitation) |
| **BUG-API-03** | `/users` | POST | Medium | Malformed JSON syntax produces unhandled `500 Internal Server Error` instead of client error `400 Bad Request`. | Open |

---

## 6. Public Practice API Limitations & Insights
1. **Stateless Mocking (Simulation)**:
   - Creating a record (`POST /users`) returns an assigned `id: 11` to simulate success. However, immediately executing `GET /users/11` returns `404 Not Found` because JSONPlaceholder does not alter its backing storage.
   - `PUT` and `DELETE` similarly simulate responses without permanent mutations.
2. **Relaxed Validation Rules**:
   - Public test beds are intentionally permissive to facilitate quick prototyping. In a real-world enterprise application, database constraints and JSON Schema validators (e.g., Joi, Express-Validator, Zod) reject empty bodies and invalid emails with `400 Bad Request`.

---

## 7. QA Conclusion
The testing suite successfully achieved full test coverage across CRUD operations and boundary conditions. All test cases have been thoroughly executed, documented, and structured for presentation in a professional QA testing portfolio.
