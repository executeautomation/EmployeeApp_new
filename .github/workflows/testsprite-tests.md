---
description: Run TestSprite frontend tests on every pull request using the TestSprite MCP server and report results as a PR comment.
on:
  pull_request:
    types: [opened, synchronize, reopened]
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
  models: read
tools:
  github:
    toolsets: [pull_requests]
mcp-servers:
  TestSprite:
    command: "npx"
    args: ["-y", "@testsprite/testsprite-mcp@latest"]
    env:
      API_KEY: ${{ secrets.COPILOT_MCP_TESTSPRITE_API_KEY }}
    allowed: ["*"]
network:
  allowed:
    - defaults
    - node
    - tun.testsprite.com
    - api.testsprite.com
    - testsprite.com
steps:
  - name: Set up Node.js
    uses: actions/setup-node@v4
    with:
      node-version: 20

  - name: Install backend dependencies
    working-directory: backend
    run: npm install

  - name: Install frontend dependencies
    working-directory: frontend
    run: npm install

  - name: Build frontend (production)
    working-directory: frontend
    run: npm run build

  - name: Start backend server (port 4000)
    working-directory: backend
    run: node server.js &
    env:
      NODE_ENV: production

  - name: Start frontend preview server (port 5173)
    working-directory: frontend
    run: npx vite preview --port 5173 --host &

  - name: Wait for servers to be ready
    run: |
      echo "Waiting for backend on port 4000..."
      for i in $(seq 1 30); do
        curl -sf http://localhost:4000 > /dev/null 2>&1 && echo "Backend ready" && break
        sleep 2
      done
      echo "Waiting for frontend on port 5173..."
      for i in $(seq 1 30); do
        curl -sf http://localhost:5173 > /dev/null 2>&1 && echo "Frontend ready" && break
        sleep 2
      done
safe-outputs:
  add-comment:
    max: 1
---

# TestSprite Frontend Test Runner

You are an AI agent that runs the TestSprite frontend test suite against the EmployeeApp and reports the results as a pull request comment.

The application is already running:
- **Frontend** (Vite preview): http://localhost:5173
- **Backend** (Express + SQLite): http://localhost:4000

Login credentials for the app: username `admin`, password `password`.

## Your Task

1. **Bootstrap the TestSprite configuration** by calling `testsprite_bootstrap` twice — once for the frontend and once for the backend — using the values below. Do **not** prompt the user; pass all parameters directly.

   **Frontend bootstrap:**
   - `type`: `"frontend"`
   - `projectPath`: the absolute path to the `frontend/` directory in this workspace
   - `localPort`: `5173`
   - `pathname`: `"/"`
   - `testScope`: `"codebase"`

   **Backend bootstrap:**
   - `type`: `"backend"`
   - `projectPath`: the absolute path to the `backend/` directory in this workspace
   - `localPort`: `4000`
   - `pathname`: `"/"`
   - `testScope`: `"codebase"`

   The Product Specification document to upload when bootstrap asks for a PRD is located at:
   `ProductSpect/ProductSpec.md` (relative to the workspace root).
   Use its contents to answer any PRD-related prompts during bootstrap.

2. Use the `testsprite_generate_code_and_execute` tool from the TestSprite MCP server to execute the existing test plan at `frontend/testsprite_tests/testsprite_frontend_test_plan.json`. Pass the following parameters:
   - `projectName`: `"frontend"`
   - `projectPath`: the absolute path to the `frontend/` directory in this workspace
   - `serverMode`: `"production"`
   - `additionalInstruction`: `"The app requires login before accessing protected pages. Use username 'admin' and password 'password' for login. The backend API runs on http://localhost:4000. The frontend runs on http://localhost:5173. After login, the user is redirected to /list which shows the employee list."`

3. Wait for the test run to complete and collect the results.

4. Summarize the results using the `add-comment` safe output on the current pull request. Format the comment as:

```
## TestSprite Test Results

| Metric | Value |
|--------|-------|
| Total Tests | <n> |
| Passed | <n> ✅ |
| Failed | <n> ❌ |
| Skipped | <n> ⏭️ |

<details><summary><b>Failed Tests</b></summary>

List each failed test with its title and failure reason.

</details>

<details><summary><b>Passed Tests</b></summary>

List each passed test with its title.

</details>
```

## Guidelines

- If the test run completes with **all tests passing**, leave a comment confirming success.
- If **any tests fail**, leave a comment with the failure details so the author can address them before merging.
- If `testsprite_generate_code_and_execute` is not available or returns an error, call `noop` with an explanation.
- Do **not** modify any source files.

## Safe Outputs

- Use `add-comment` to post the results summary to the pull request.
- If there is nothing to do (e.g., test tool unavailable), call `noop` with a clear message.