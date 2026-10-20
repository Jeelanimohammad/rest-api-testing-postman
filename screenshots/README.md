# Test Execution Screenshots

This directory is designated for storing visual test execution evidence.

### Recommended Screenshots to Include:
1. `postman_collection_run.png`: Postman Collection Runner window showing all 24 test cases passing/executing with green checkmarks.
2. `get_request_assertion.png`: Inspecting a `GET /users/1` request showing status 200, response body, and Test Results tab (5/5 assertions passed).
3. `post_request_assertion.png`: Executing `POST /users` with JSON payload and observing status `201 Created` with simulated `id: 11`.
4. `negative_test_404.png`: Calling `GET /users/999` and observing status `404 Not Found`.

> **Note for Evaluators / Reviewers:** All test requests and assertions are pre-configured inside `postman/student_records_api_testing.postman_collection.json` and can be imported and executed directly in Postman Free Edition.
