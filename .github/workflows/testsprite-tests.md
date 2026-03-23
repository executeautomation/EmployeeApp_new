---
description: Run TestSprite frontend tests on every pull request using the TestSprite MCP server and report results as a PR comment.
on:
  pull_request:
    types: [opened, synchronize, reopened]
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
tools:
  github:
    toolsets: [pull_requests]
mcp-servers:
  TestSprite:
    command: "npx"
    args: ["-y", "@testsprite/testsprite-mcp@latest"]
    allowed: ["*"]
    env:
      API_KEY: ${{ secrets.COPILOT_MCP_TESTSPRITE_API_KEY }}
    
network:
  allowed:
    - defaults
    - node
    - python
    - tun.testsprite.com
    - api.testsprite.com
    - testsprite.com
    - playwright.azureedge.net
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

Follow these steps **in order**. Each step depends on the previous one completing successfully.

### Step 1 — Bootstrap the project

Use the `testsprite_bootstrap` tool to initialize TestSprite for this project. Pass the following parameters:
- `projectName`: `"frontend"`
- `projectPath`: the absolute path to the `frontend/` directory in this workspace
- `type`: `"frontend"`
- `localEndpoint`: `"http://localhost:5173/login"`
- `loginUser`: `"admin"`
- `loginPassword`: `"password"`
- `prdContent`: the full contents of the file `ProductSpect/ProductSpec.md` from the workspace (read it first)

### Step 2 — Generate code summary

Use the `testsprite_generate_code_summary` tool to analyze the codebase:
- `projectName`: `"frontend"`
- `projectPath`: the absolute path to the `frontend/` directory in this workspace

### Step 3 — Generate standardized PRD

Use the `testsprite_generate_standardized_prd` tool:
- `projectName`: `"frontend"`
- `projectPath`: the absolute path to the `frontend/` directory in this workspace

### Step 4 — Generate frontend test plan

Use the `testsprite_generate_frontend_test_plan` tool:
- `projectName`: `"frontend"`
- `projectPath`: the absolute path to the `frontend/` directory in this workspace

### Step 5 — Execute the tests

Use the `testsprite_generate_code_and_execute` tool to run all generated tests:
- `projectName`: `"frontend"`
- `projectPath`: the absolute path to the `frontend/` directory in this workspace
- `serverMode`: `"production"`
- `additionalInstruction`: `"The app requires login before accessing protected pages. Use username 'admin' and password 'password' for login. The backend API runs on http://localhost:4000. The frontend runs on http://localhost:5173. After login, the user is redirected to /list which shows the employee list."`

### Step 6 — Report results

Summarize the test results using the `add-comment` safe output on the current pull request. Format the comment as:

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

- Follow the steps sequentially — do not skip steps or run them out of order.
- If the test run completes with **all tests passing**, leave a comment confirming success.
- If **any tests fail**, leave a comment with the failure details so the author can address them before merging.
- If any tool is not available or returns an error, call `noop` with an explanation.
- Do **not** call `testsprite_open_test_result_dashboard` — this is a headless CI environment with no display server.
- Do **not** modify any source files.

## Safe Outputs

- Use `add-comment` to post the results summary to the pull request.
- If there is nothing to do (e.g., test tool unavailable), call `noop` with a clear message.
