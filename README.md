# Lab 1 - GitHub Actions

A small Express app for the CI/CD lab, using Node.js 24 and Yarn 4.

## Run

```sh
corepack enable
corepack prepare yarn@4.18.1 --activate
yarn install --immutable
yarn start
```

Open http://localhost:3000/. It should show `Hello, GitHub Actions!`.
The `/health` route returns `{ "status": "ok" }`.

## Check

```sh
yarn lint
yarn test
yarn coverage
```

GitHub Actions runs these checks on pushes to `main` and pull requests.

[Step-by-step notes](STEPS.md)
