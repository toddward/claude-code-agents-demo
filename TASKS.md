# TASKS.md

Work through these tasks in order. Each task builds on the previous one.

---

## Task 1: Project Setup

Initialize the Node.js project and install dependencies.

- [ ] Run `npm init -y`
- [ ] Install Express: `npm install express`
- [ ] Install dev dependencies: `npm install -D vitest supertest`
- [ ] Add scripts to `package.json`:
  - `"start": "node server.js"`
  - `"test": "vitest run"`
  - `"test:watch": "vitest"`

---

## Task 2: Build the Task Management API

Create `server.js` with the following endpoints. Store tasks in an in-memory array. Each task has: `id` (UUID), `title` (string, required), `description` (string, optional), `status` (enum: `pending`, `in-progress`, `done`, default `pending`), `createdAt`, `updatedAt`.

### Endpoints

| Method   | Path          | Description              |
|----------|---------------|--------------------------|
| `GET`    | `/tasks`      | List all tasks           |
| `POST`   | `/tasks`      | Create a new task        |
| `GET`    | `/tasks/:id`  | Get a task by ID         |
| `PUT`    | `/tasks/:id`  | Update a task            |
| `DELETE` | `/tasks/:id`  | Delete a task            |
| `GET`    | `/health`     | Health check endpoint    |

### Requirements

- Return JSON responses with a consistent envelope: `{ data }` for success, `{ error }` for errors
- Use appropriate HTTP status codes (200, 201, 204, 400, 404)
- Validate that `title` is present and non-empty on POST
- Validate that `status` is one of the allowed values on PUT
- Export the Express app for testing (`module.exports = app`)

---

## Task 3: Security Review

Invoke the **Security Reviewer** agent to audit `server.js`.

- [ ] Ask: "Review server.js for security vulnerabilities"
- [ ] Address any CRITICAL or HIGH findings
- [ ] Re-run the review to confirm fixes

---

## Task 4: API Design Review

Invoke the **API Architect** agent to review the API design.

- [ ] Ask: "Review the API design of server.js"
- [ ] Implement recommended improvements
- [ ] Re-run the review to confirm the design maturity rating improved

---

## Task 5: Write Tests

Invoke the **Test Strategist** agent to design a test plan.

- [ ] Ask: "Design a test strategy for server.js"
- [ ] Create `server.test.js` implementing the top 5 recommended tests
- [ ] Run `npm test` and ensure all tests pass

---

## Task 6: Generate Documentation

Invoke the **Doc Writer** agent to generate API documentation.

- [ ] Ask: "Generate API documentation for this project"
- [ ] Review the generated docs and make any adjustments
- [ ] Ensure curl examples are accurate and runnable
