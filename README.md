# Deployment Exercise 2 (deployment2.yml)

## Description:
Automates linting, testing, building, and deploying the basics-exercise Node.js project on every push (except changes in certain workflow files).

## Workflow Steps:

**Lint:** Checks code style using `npm run lint`.

**Test:** Runs tests with `npm run test`.

**Deploy:** Builds the project using `npm run build` and simulates deployment with `echo "Deploying ..."`.

## Usage / Notes:

Dependencies are installed automatically:

* Use `npm ci` if `package-lock.json` exists.
* Otherwise, use `npm install`.

Workflow triggers on push, ignoring:

* `.github/workflows/deployment1.yml`
* `.github/workflows/deployment.yml`
* `.github/workflows/demo1.yml`
* `.github/workflows/demo.yml`
