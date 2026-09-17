[ReadME.md](https://github.com/user-attachments/files/32325772/ReadME.md)
# Api-Testing-Portfolio
Automated API testing suite built with Postman and Newman. It creates, reads, updates, and deletes user profiles while testing server responses for speed and accuracy.
# User Management API Regression Suite (Postman & Newman)

An automated API test automation framework built with **Postman** and **Newman** for functional regression testing of user management endpoints against the [ReqRes REST API](https://reqres.in/).

---

## 📌 Project Overview

This portfolio project demonstrates automated API end-to-end testing, dynamic variable passing, response validation, and command-line test execution.

* **Target API:** ReqRes REST API (`https://reqres.in/api`)
* **Test Tooling:** Postman (GUI Development) & Newman CLI (Automated Test Execution)
* **Scripting:** JavaScript (`pm.*` assertions, JSON schema/body validation)
* **Key Concept:** Dynamic Data Chaining (Extracting created user IDs from POST responses to drive subsequent PUT and DELETE requests).

---

## 🧪 Test Suite Details & Workflow

The regression collection executes requests sequentially to validate full CRUD operation lifecycles:

1. **`GET /users/2` (Fetch User Profile)**
   * **Assertions:**
     * Status code is `200 OK`.
     * Response time is less than `1000ms`.
     * Response body contains target user schema (`id`, `email`, `first_name`, `last_name`, `avatar`).

2. **`POST /users` (Create User)**
   * **Assertions:**
     * Status code is `201 Created`.
     * Body returns specified job title and name.
   * **Dynamic Scripting:**
     * Extracts `id` from the response payload and sets a global runtime variable `new_user_id`.

3. **`PUT /users/{id}` (Update User)**
   * **Assertions:**
     * Uses dynamic variable `{{new_user_id}}` in request path.
     * Status code is `200 OK`.
     * Confirms updated `job` title property.

4. **`DELETE /users/{id}` (Delete User)**
   * **Assertions:**
     * Uses dynamic variable `{{new_user_id}}` in request path.
     * Status code is `204 No Content`.

---

## 🛠️ Prerequisites & Setup

### Requirements
* [Node.js](https://nodejs.org/) (v16.x or higher)
* [Postman](https://www.postman.com/) (for visual editing)

### Installing Newman
To run the automated suite headlessly via terminal:

```bash
npm install -g newman
```

Verify installation:
```bash
newman -v
```

---

## 🚀 How to Run the Tests

### 1. Clone or Download Repository
```bash
git clone https://github.com/your-username/user-management-api-tests.git
cd user-management-api-tests
```

### 2. Run via Newman CLI
Execute the exported Postman collection directly:

```bash
newman run MyCollection.json
```

---

## 📊 Example CLI Execution Output

```text
User Management API Regression Suite

→ Fetch a Single User Profile
  GET https://reqres.in/api/users/2 [200 OK, 185B, 240ms]
  ✓ Status code is 200
  ✓ Response time is less than 1000ms
  ✓ Response contains data for user 2

→ Create User
  POST https://reqres.in/api/users [201 Created, 210B, 310ms]
  ✓ Status code is 201 Created
  ✓ Verify job is saved correctly

→ Update User
  PUT https://reqres.in/api/users/482 [200 OK, 195B, 290ms]
  ✓ Status code is 200
  ✓ Verify updated job title

→ Delete User
  DELETE https://reqres.in/api/users/482 [204 No Content, 0B, 220ms]
  ✓ Status code is 204 No Content

┌─────────────────────────┬──────────┬──────────┐
│                         │ executed │   failed │
├─────────────────────────┼──────────┼──────────┤
│              iterations │        1 │        0 │
├─────────────────────────┼──────────┼──────────┤
│                requests │        4 │        0 │
├─────────────────────────┼──────────┼──────────┤
│            test-scripts │        8 │        0 │
├─────────────────────────┼──────────┼──────────┤
│              assertions │        8 │        0 │
└─────────────────────────┴──────────┴──────────┘
Total run duration: 1060ms
```

---

## 📁 Repository Structure

```text
├── MyCollection.json    # Exported Postman Collection v2.1 containing requests & scripts
└── README.md            # Project documentation & setup instructions
```
