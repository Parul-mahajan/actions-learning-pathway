# CI/CD Pipeline Workflow

This document describes the `build-test-deploy.yml` workflow file for our CI/CD pipeline.

## Workflow Triggers

The workflow is triggered on every push to the `main` branch.

## Jobs

The workflow consists of three jobs: `build`, `test`, and `deploy`.

### Build Job

The `build` job runs on the latest version of Ubuntu. It checks out the repository, sets up Node.js version '18.x', installs the dependencies using `npm install`, and builds the project using `npm run build`.

### Test Job

The `test` job depends on the `build` job. It runs on the latest version of Ubuntu, checks out the repository, sets up Node.js version '18.x', installs the dependencies using `npm install`, and runs the tests using `npm test`.

### Deploy Job

The `deploy` job depends on the `test` job. It runs on the latest version of Ubuntu, checks out the repository using a GitHub token, sets up Node.js version '18.x', installs the dependencies using `npm install`, and builds the project using `npm run build`.

The job then uploads the build artifacts from the './out' directory using the `actions/upload-artifact@v2` action.

Finally, the job deploys the project to GitHub Pages using the `JamesIves/github-pages-deploy-action@4.1.5` action. The branch for GitHub Pages is set to `gh-pages` and the folder to deploy is `out`.

The URL of the deployed site is available as an output of the `deploy` job.

## Outputs

The `deploy` job provides the following output:

- `url`: The URL of the deployed site.