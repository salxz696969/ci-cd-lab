# Lab 1 - What I did

## 1. Create the project

I made a `ci-cd-lab` folder with `test/` and `.github/workflows/` inside it.
I also kept a local copy of the lab PDF in `docs/`, outside Git.

## 2. Set up the tools

I used Node.js 24.22.1 and Yarn 4.18.1, as required by the lab.

## 3. Add package.json

I added Express and the testing tools. I set `"type": "module"` so I could use
`import` and `export`. I added the start, lint, test and coverage commands.

## 4. Make the app

In `app.js`, I created an Express app. The `GET /` route returns status 200
and `Hello, GitHub Actions!`. Status 200 means the request worked.

## 5. Start the server

In `server.js`, I imported the app and called `app.listen()`.
The default port is 3000. I used port 3001 locally because 3000 was already busy.
Keeping this file separate lets the tests import the app without starting it manually.

## 6. Install the packages

I used Yarn to install the dependencies. Yarn generated `yarn.lock`, which
records the dependency versions. I added it to Git with the source files.

## 7. Write the tests

I wrote two tests for `/`: one checks status 200 and the other checks the greeting.
Mocha runs the tests, Chai checks the results, and Supertest sends the requests.

## 8. Run lint and tests

I ran `yarn lint` to check the code and `yarn test` to run the tests.
Both tests passed. Then I changed the greeting on purpose. The text test failed,
but the status test still passed. I restored the greeting and ran the tests again.

## 9. Check coverage

I ran `yarn coverage` and opened `coverage/index.html`.
The app was covered, but `server.js` was not, since the tests import `app.js`.
The first whole-project line coverage result was 56.25%.

## 10. Add GitHub Actions

I created `.github/workflows/ci.yml`. It sets up Node.js and Yarn, installs
packages, runs lint and tests, and uploads the coverage report.
`yarn install --immutable` stops CI from changing the lockfile.

## 11. Push and check CI

I created the GitHub repository and pushed the project. I checked the Actions
page and downloaded the coverage report. All the checks passed.

## 12. Try a pull request

I made a feature branch and added `/health`. It returns status 200 and
`{ "status": "ok" }`. I added a test for its status, content type and body,
then opened a pull request. All three tests and the GitHub checks passed.
The final whole-project line coverage was 65%.

## What I learned

CI checks changes automatically so mistakes can be caught before merging.
This lab runs checks; it does not deploy the app. Coverage shows what the tests
executed, but even 100% coverage would not mean there are no bugs.
