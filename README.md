# REST API Testing and Validation Using Postman

![Postman](https://img.shields.io/badge/Postman-v10%2B-orange?logo=postman&logoColor=white)
![Testing Type](https://img.shields.io/badge/Testing-REST%20API-blue)
![Status](https://img.shields.io/badge/Test%20Execution-Passed%20(22%2F24)-brightgreen)
![License](https://img.shields.io/badge/License-MIT-green)

A comprehensive, industry-aligned REST API testing and validation project designed for entry-level QA Engineers and Software Test Interns. This portfolio repository showcases hands-on experience with HTTP protocols, CRUD testing, automated JavaScript assertions in Postman, negative testing, defect reporting, and test metrics analysis.

---

## 📌 Table of Contents
1. [Project Overview & Objectives](#-project-overview--objectives)
2. [Practice API Details & Mapping](#-practice-api-details--mapping)
3. [Tools & Technologies](#-tools--technologies)
4. [API Endpoints Tested](#-api-endpoints-tested)
5. [Repository Structure](#-repository-structure)
6. [How to Import and Run the Postman Collection](#-how-to-import-and-run-the-postman-collection)
7. [Postman Test Assertions Explained](#-postman-test-assertions-explained)
8. [Test Execution Summary](#-test-execution-summary)
9. [Defects Found & API Limitations](#-defects-found--api-limitations)
10. [Key QA Concepts Learned](#-key-qa-concepts-learned)
11. [QA Interview Q&A Guide](#-qa-interview-qa-guide)

---

## 🎯 Project Overview & Objectives

In modern web architecture, REST APIs form the backbone connecting client interfaces to backend microservices and databases. The objective of this project is to validate RESTful endpoints using **Postman Free Edition**, ensuring data integrity, correct HTTP status codes, performance benchmarks, and graceful negative error handling.

### Core Objectives:
- Master REST API architecture, HTTP verbs, and JSON payloads.
- Test standard **CRUD operations** (Create, Read, Update, Delete) against a public API.
- Implement reusable **JavaScript assertions** within Postman (`pm.test`, `pm.expect`).
- Conduct thorough **Negative Testing** (404 errors, malformed payloads, invalid IDs).
- Record and track 24 test scenarios in a structured CSV test suite.
- Document genuine defects and public sandbox mock limitations.

---

## 🌐 Practice API Details & Mapping

- **API Provider:** [JSONPlaceholder](https://jsonplaceholder.typicode.com)
- **Base URL:** `https://jsonplaceholder.typicode.com`
- **Domain Adaptation:** Tested the `/users` resource mapped conceptually to **Student / Candidate Records** (`Student Records API Testing`).
- **Authentication:** None required (Publicly accessible, zero-cost, no API key needed).

### ⚠️ Public Mock API Limitations (Important QA Distinction):
1. **Stateless Simulation:** `POST`, `PUT`, and `DELETE` requests succeed and return realistic response bodies (e.g., `POST` returns `id: 11`), but **changes are not permanently persisted** to the underlying database. Querying the record immediately after (`GET /users/11`) will return `404 Not Found`.
2. **Permissive Validation:** Unlike production backends that enforce strict schema validators (e.g., rejecting empty bodies with `400 Bad Request`), JSONPlaceholder accepts empty objects `{}` and unformatted emails to ease rapid prototyping.

---

## 🛠️ Tools & Technologies

- **API Client:** Postman (Free Edition)
- **Data Exchange Format:** JSON (JavaScript Object Notation)
- **Scripting:** JavaScript (Chai Assertion Library via Postman Sandbox)
- **Version Control:** Git & GitHub

---

## 📋 API Endpoints Tested

| Resource | HTTP Method | Endpoint | Description |
| :--- | :--- | :--- | :--- |
| **Users** | `GET` | `/users` | Retrieve all student/user records |
| **Users** | `GET` | `/users/:id` | Retrieve single student by ID (e.g., `/users/1`) |
| **Users** | `GET` | `/users?username=Bret` | Filter records by query parameter |
| **Users** | `POST` | `/users` | Create a new student record (JSON payload) |
| **Users** | `PUT` | `/users/:id` | Full update of existing record |
| **Users** | `PATCH` | `/users/:id` | Partial update of specific fields |
| **Users** | `DELETE`| `/users/:id` | Remove a record |
| **Negative** | `GET` | `/users/999` | Non-existent record validation |
| **Negative** | `GET` | `/invalid_students` | Non-existent route validation |

---

## 📂 Repository Structure

```text
rest-api-testing-postman/
│
├── README.md                                             # Comprehensive project documentation
│
├── postman/
│   └── student_records_api_testing.postman_collection.json # Exported Postman collection with tests
│
├── test-cases/
│   └── api_test_cases.csv                                # 24 detailed test cases (Excel-compatible)
│
├── bug-reports/
│   ├── defect_report_template.csv                        # Standard QA bug logging template
│   └── defects_found.csv                                 # Genuine bugs & observed mock limitations
│
├── reports/
│   └── test_execution_summary.md                         # Full test execution report & metrics
│
└── screenshots/
    └── README.md                                         # Visual test evidence placeholders & guide
```

---

## 🚀 How to Import and Run the Postman Collection

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Jeelanimohammad/rest-api-testing-postman.git
   ```
2. **Launch Postman** on your computer.
3. Click the **Import** button in the top-left corner of Postman.
4. Drag and drop `postman/student_records_api_testing.postman_collection.json` or browse to select it.
5. Once imported, you will see the collection named **`Student Records API Testing`** organized into 5 structured folders:
   - 📁 `GET Request Tests`
   - 📁 `POST Request Tests`
   - 📁 `PUT Request Tests`
   - 📁 `DELETE Request Tests`
   - 📁 `Negative Tests`
6. **Run the Collection:**
   - Click on the collection name **Student Records API Testing**.
   - Click the **Run** button (Collection Runner).
   - Click **Run Student Records API Testing**.
   - Observe real-time test execution results and assertion pass/fail statuses.

---

## 💻 Postman Test Assertions Explained

All requests in the collection utilize Postman's built-in `pm.*` JavaScript testing library.

### 1. HTTP Status Code Assertion
```javascript
// Confirms that the server responded with 200 OK
pm.test("Status code is 200 OK", function () {
    pm.response.to.have.status(200);
});
```
*Explanation:* `pm.response.to.have.status(200)` checks if the response code matches `200`. For record creation, we assert `201`.

### 2. Header and Response Format Validation
```javascript
// Verifies response is returned in JSON format
pm.test("Content-Type header is JSON", function () {
    pm.expect(pm.response.headers.get("Content-Type")).to.include("application/json");
});
```
*Explanation:* Inspects the HTTP response headers to ensure the server communicated in standard `application/json`.

### 3. Response Latency Assertion
```javascript
// Enforces API performance SLA
pm.test("Response time is under 1500ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(1500);
});
```
*Explanation:* Validates that the round-trip network response is under 1.5 seconds, catching API bottlenecks.

### 4. JSON Schema and Field Assertion
```javascript
// Validates expected fields exist and data types match
pm.test("Record contains valid schema fields", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.id).to.eql(1);
    pm.expect(jsonData.name).to.be.a("string");
    pm.expect(jsonData.address).to.be.an("object");
});
```
*Explanation:* Parses the response string into a JavaScript object via `pm.response.json()` and checks specific field types.

---

## 📊 Test Execution Summary

| Metric | Result |
| :--- | :--- |
| **Total Test Cases** | 24 |
| **Passed Tests** | 22 (91.7%) |
| **Failed Tests** | 2 (8.3%) *(Schema validation bypassed by practice mock)* |
| **Blocked / Not Run** | 0 |
| **Defects Logged** | 3 |

*Detailed breakdown available in [reports/test_execution_summary.md](reports/test_execution_summary.md).*

---

## 🐛 Defects Found & API Limitations

| Bug ID | Endpoint | Method | Observed Behavior | Expected Production Behavior | Severity |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **BUG-API-01** | `/users` | POST | Submitting `{}` returned `201 Created` | Reject missing fields with `400 Bad Request` | Medium |
| **BUG-API-02** | `/users` | POST | Submitting invalid email returned `201 Created` | Validate email format with `400 Bad Request` | Low |
| **BUG-API-03** | `/users` | POST | Malformed JSON caused `500 Internal Server Error` | Return `400 Bad Request` on invalid client syntax | Medium |

---

## 🎓 Key QA Concepts Learned

1. **Client-Server Communication:** Understanding headers, status codes, query parameters, and payload formatting.
2. **API Verification vs UI Verification:** API testing validates backend business logic and database integrity before frontend UI integration occurs, leading to earlier defect detection.
3. **Idempotence:** Learning that `GET`, `PUT`, and `DELETE` are idempotent (repeated calls produce the same system state), whereas `POST` is not.
4. **Mock vs Production:** Recognizing the difference between simulated sandbox backends and real production APIs with persistent state and strict validators.

---

## 💡 QA Interview Q&A Guide

#### 1. What is an API and why is API testing important?
> **Answer:** API stands for Application Programming Interface. It acts as an intermediary enabling different software systems to communicate. API testing is crucial because it validates business logic, security, and data integrity at the transport layer before the UI is built, catching defects earlier when they are cheaper to fix.

#### 2. What is the difference between GET and POST?
> **Answer:** `GET` is used to retrieve data from a server; it does not contain a request body and should be safe and idempotent. `POST` is used to send data to the server to create a new resource; it includes a request body (typically JSON) and is non-idempotent.

#### 3. What is the difference between PUT and PATCH?
> **Answer:** `PUT` replaces the entire target resource with the new request data. `PATCH` applies partial modifications, updating only the specific fields supplied in the request body while preserving the rest.

#### 4. What are the common HTTP status code ranges?
> **Answer:**
> - **2xx (Success):** `200 OK`, `201 Created`, `204 No Content`
> - **3xx (Redirection):** `301 Moved Permanently`, `304 Not Modified`
> - **4xx (Client Errors):** `400 Bad Request`, `401 Unauthorized`, `403 Forbidden`, `404 Not Found`
> - **5xx (Server Errors):** `500 Internal Server Error`, `502 Bad Gateway`, `503 Service Unavailable`

#### 5. How did you handle negative testing in your project?
> **Answer:** I tested invalid record IDs (e.g., `/users/999`, `/users/-1`), non-existent endpoints (`/invalid_students`), malformed JSON syntax, and empty payload submissions to observe how the server handles unexpected client input.

---

## 👤 Author
**Mohammad Jeelani**  
- GitHub: [@Jeelanimohammad](https://github.com/Jeelanimohammad)
- Project Repository: [rest-api-testing-postman](https://github.com/Jeelanimohammad/rest-api-testing-postman)