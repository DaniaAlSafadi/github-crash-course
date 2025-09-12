# GitHub Actions Workflows
## GitHub Actions Workflows Overview

| # | Workflow Name | File | Triggers | Main Steps |
|---|---------------|------|----------|------------|
| 1 | First Workflow | first-action.yml | workflow_dispatch | Print greeting, Print goodbye |
| 2 | Output Information | output.yml | workflow_dispatch | Output GitHub context |
| 3 | Handle Issues | issues.yml | issues | Output event details |
| 4 | Deploy Project | deployment.yml | push (ignoring certain workflows), workflow_dispatch | Install dependencies, Test, Build, Deploy |
| 5 | Deployment Exercise 1 | deployment1.yml | push (ignoring certain workflows) | Get code, Install dependencies, Lint, Test, Build, Deploy |
| 6 | Deployment Exercise 2 | deployment2.yml | push (ignoring certain workflows) | Lint, Install dependencies, Test, Build, Deploy |
---

## 1. First Workflow (`first-action.yml`)

**Description**  
The very first workflow project — a simple job that prints a greeting and a goodbye message when manually triggered.

**Workflow Steps**

1. **Print greeting:**  
   - Runs `echo "Hello World!"`  

2. **Print goodbye:**  
   - Runs `echo "Done - bye!"`  

**Usage / Notes**

- Triggered manually via `workflow_dispatch`.  
- Serves as an introductory example of GitHub Actions.  
- **History:** This was the first project created to get started with GitHub Actions.

---

## 2. Output Information (`output.yml`)

**Description**  
A workflow that prints the entire GitHub context object when triggered manually.

**Workflow Steps**

1. **Output GitHub context:**  
   - Runs `echo "${{ toJSON(github) }}"`.  

**Usage / Notes**

- Triggered manually via `workflow_dispatch`.  
- Useful for inspecting available GitHub context variables.  

---

## 3. Handle Issues (`issues.yml`)

**Description**  
A workflow that triggers whenever a GitHub Issue event occurs, and outputs the full event details.

**Workflow Steps**

1. **Output event details:**  
   - Runs `echo "${{ toJSON(github.event) }}"`.  

**Usage / Notes**

- Triggered automatically on `issues` events.  
- Useful for debugging issue-related automation.  

---

## 4. Deploy Project (`deployment.yml`)

**Description**  
Runs tests and deploys the `second-action-react-demo` Node.js project on push or manually via `workflow_dispatch`.

**Workflow Steps**

1. **Test:**  
- Checks out the repository code using `actions/checkout@v4`.  
- Sets up Node.js version 18.  
- Installs dependencies using `npm ci` if `package-lock.json` exists, otherwise `npm install`.  
- Runs tests with `npm test`.  

2. **Deploy:**  

🔴 Runs after the test job completes successfully.

   - Checks out the repository code again.  
   - Sets up Node.js version 18.  
   - Installs dependencies.  
   - Builds the project using `npm run build`.  
   - Simulates deployment with `echo "Deploying ..."`.

**Usage / Notes**

- Dependencies are installed automatically.  
- Workflow triggers on push, ignoring:
  - `.github/workflows/deployment1.yml`
  - `.github/workflows/deployment2.yml`
  - `.github/workflows/demo1.yml`
  - `.github/workflows/demo.yml`
- Can also be triggered manually via `workflow_dispatch`.

---

## 5. Deployment Exercise 1 (`deployment1.yml`)

**Description**  
Automates linting, testing, building, and deploying the `basics-exercise` Node.js project on every push (except changes in certain workflow files).

**Workflow Steps**

1. **Deploy:**
  - Checks out the repository code using `actions/checkout@v3`.  
   - Installs dependencies in `basics-exercise`.  
   - Uses `npm ci` if `package-lock.json` exists, otherwise `npm install`.  
   - Runs `npm run lint` to check code style.  
   - Runs tests with `npm run test`.  
   - Builds the project using `npm run build`.  
   - Simulates deployment with `echo "Deploying ..."`.

**Usage / Notes**

- Workflow triggers on push, ignoring:
  - `.github/workflows/deployment.yml`
  - `.github/workflows/deployment2.yml`
  - `.github/workflows/demo1.yml`
  - `.github/workflows/demo.yml`
 
  ---

## 6. Deployment Exercise 2 (`deployment2.yml`)

**Description**  
Automates linting, testing, building, and deploying the `basics-exercise` Node.js project on every push, excluding changes in certain workflow files.

**Workflow Steps**

1. **Lint:**
  
   - Checks out the repository code using `actions/checkout@v3`.  
   - Installs dependencies in `basics-exercise`.  
     - Uses `npm ci` if `package-lock.json` exists, otherwise `npm install`.  
   - Runs `npm run lint` to check code style.  

3. **Test:**  

🔴 Runs after the lint job completes successfully.

   - Checks out the repository code using `actions/checkout@v3`.  
   - Installs dependencies.  
   - Runs tests with `npm run test`.  

3. **Deploy:**  

🔴 Runs after the test job completes successfully.

   - Checks out the repository code using `actions/checkout@v3`.  
   - Installs dependencies.  
   - Builds the project using `npm run build`.  
   - Simulates deployment with `echo "Deploying ..."`.

**Usage / Notes**

- Dependencies are installed automatically.  
- Workflow triggers on push, ignoring:
  - `.github/workflows/deployment1.yml`
  - `.github/workflows/deployment.yml`
  - `.github/workflows/demo1.yml`
  - `.github/workflows/demo.yml`
 
---
