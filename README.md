## GitHub Actions Workflows Overview

| # | Workflow Name | File | Triggers | Main Steps |
|---|---------------|------|----------|------------|
| 1 | Deploy Project | deployment.yml | push (ignoring certain workflows), workflow_dispatch | Test, Deploy |
| 2 | Deployment Exercise 1 | deployment1.yml | push (ignoring certain workflows) | Get code, Install dependencies, Lint, Test, Build, Deploy |
| 3 | Deployment Exercise 2 | deployment2.yml | push (ignoring certain workflows), workflow_dispatch | Test, Deploy |

---

## 1. Deploy Project (deployment.yml)

**Description**  
Runs tests and deploys the `second-action-react-demo` Node.js project on push or manually via `workflow_dispatch`.

**Workflow Steps**

1. **Test:**  
   - Checks out the repository code using `actions/checkout@v4`.  
   - Sets up Node.js version 18.  
   - Installs dependencies using `npm ci` if `package-lock.json` exists, otherwise `npm install`.  
   - Runs tests with `npm test`.  

2. **Deploy:**  
   - Runs after the test job completes successfully.  
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


## 2. Deployment Exercise 1 (deployment1.yml)

**Description**  
Automates linting, testing, building, and deploying the `basics-exercise` Node.js project on every push (except changes in certain workflow files).

**Workflow Steps**

1. **Get code:**  
   - Checks out the repository code using `actions/checkout@v3`.

2. **Install dependencies:**  
   - Installs Node.js dependencies in `basics-exercise`.  
   - Uses `npm ci` if `package-lock.json` exists, otherwise `npm install`.

3. **Lint:**  
   - Runs `npm run lint` to check code style.

4. **Test code:**  
   - Runs tests with `npm run test`.

5. **Build code:**  
   - Builds the project using `npm run build`.

6. **Deploy code:**  
   - Simulates deployment with `echo "Deploying ..."`.

**Usage / Notes**

- Workflow triggers on push, ignoring:
  - `.github/workflows/deployment.yml`
  - `.github/workflows/deployment2.yml`
  - `.github/workflows/demo1.yml`
  - `.github/workflows/demo.yml`


## 3. Deployment Exercise 2 (deployment2.yml)

**Description**  
Automates linting, testing, building, and deploying the `second-action-react-demo` Node.js project on every push (except changes in certain workflow files) and can also be triggered manually.

**Workflow Steps**

1. **Test:**  
   - Checks out the repository code.  
   - Sets up Node.js version 18.  
   - Installs dependencies using `npm ci` if `package-lock.json` exists, otherwise `npm install`.  
   - Runs tests with `npm test`.  

2. **Deploy:**  
   - Runs after the test job completes successfully.  
   - Checks out the repository code again.  
   - Sets up Node.js version 18.  
   - Installs dependencies.  
   - Builds the project using `npm run build`.  
   - Simulates deployment with `echo "Deploying ..."`.

**Usage / Notes**

- Dependencies are installed automatically as part of each job.  
- Workflow triggers on push, ignoring:
  - `.github/workflows/deployment1.yml`
  - `.github/workflows/deployment2.yml`
  - `.github/workflows/demo1.yml`
  - `.github/workflows/demo.yml`
- Workflow can also be triggered manually via `workflow_dispatch`.
