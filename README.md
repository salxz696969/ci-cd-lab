# Lab 1: Building a CI/CD pipeline with GitHub Actions

An ES Module application using Node.js 24, Yarn 4, Express 5, Mocha, Chai,
Supertest, ESLint and c8, implemented from the supplied lab handout.

## Run the lab

Install Node.js 24 or later and Corepack, then run:

```sh
corepack enable
corepack prepare yarn@4.18.1 --activate
yarn install --immutable
yarn lint
yarn test
yarn coverage
yarn start
```

Visit http://localhost:3000/. The response is `Hello, GitHub Actions!`.
Set `PORT` to choose another port. Open `coverage/index.html` for the HTML report.
The lockfile is committed; generated reports and dependencies are ignored.

## How it works

`app.js` defines and exports the Express application. `server.js` starts its
listener. Tests import the application directly, so they do not require a
separate server process. Mocha runs the tests, Chai makes assertions, and
Supertest performs HTTP requests against the application.

`eslint.config.js` enables recommended ESLint checks and the Node.js and Mocha
globals. `.yarnrc.yml` selects a conventional `node_modules` install.

The workflow runs for pushes to `main`, pull requests targeting `main`, and
manual dispatch. It activates the pinned Yarn version before the cache lookup,
sets up Node.js 24, performs an immutable install, runs lint, tests and coverage,
and uploads `code-coverage-report` as a downloadable artifact.

## Coverage

c8 reports statements, branches, functions and lines. Both `app.js` and
`server.js` are included, even if a file is never imported by tests. This avoids
hiding the untested server bootstrap. No optional minimum threshold is enforced;
the report explains the actual measured results. Coverage does not prove that
all requirements or edge cases are correct.

## CI, delivery and deployment

Continuous integration validates changes automatically. Continuous delivery
keeps tested changes ready for a release, usually with manual approval.
Continuous deployment automatically releases every approved-by-checks change
to a target environment. This lab implements CI and publishes a coverage
artifact; it does not deploy the application.

## Lab evidence

See `docs/LAB-REPORT.md` for the procedure, explanations, observed results,
intentional failing-test experiment, and GitHub evidence. A copy of the
original assignment is stored in `docs/`.
