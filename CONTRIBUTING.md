# Contributing

Quick guide for keeping work consistent as a team.

Continuing from A1 - Commits follow [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) (with the Jira ticket as the scope), and we use [GitHub Flow](https://docs.github.com/en/get-started/using-github/github-flow) for branching: short-lived branches off `main`, merged back through a reviewed PR.

## Setup

1. Clone the repo and install everything from the root
2. Copy `backend/.env.example` to `backend/.env` and fill in your own values. Never commit your `.env`
    - `MONGO_URI`: provided by Xander
        - If having access issues, your IP probably needs to be added to the whitelist
        - `MONGO_URI` should never be pointed to the prod db
    - `JWT_SECRET`:  any random long string
        - or generate:
          `openssl rand -base64 32`
    - Seed logins (`ORGANISER_*`, `ATTENDEE_*`): use the shared test values from OneDrive so everyone tests with the same accounts. Don't put them in `.env.example`
3. (Optional) Seed test data
    ```bash
    cd backend
    npm run reset
    ```
4. Run the app from the root:
    ```bash
    npm run dev
    ```

## Branches

- `main` is protected, all changes go through a PR.
- Branch off `main` and name it after the Jira ticket:
  
  eg
    - `feature/A2-01-short-description`
    - `fix/A2-02-short-description`
    - `docs/A2-03-short-description`
    - `test/A2-04-short-description`
    - `chore/A2-05-short-description`
- Pull the latest `main` before starting a new branch.

## Commits

Keep commits small and include the Jira ticket in brackets after the prefix, so the commit shows up on the ticket in Jira:

```
type(TICKET): short description
```

eg

- `feat(A2-01): add edit event form`
- `fix(A2-02): validate rating range`
- `docs(A2-03): update README setup steps`
- `test(A2-04): add feedback controller tests`
- `chore(A2-05): update dependencies`
- `style(A2-06): format with prettier`

Use the same ticket for the branch you're working on. If a change isn't tied to a ticket, leave the brackets off.

This way your Jira ticket will have commits, branch, and PR.

## Tests

- Backend tests live in `backend/test/`.

## Postman

- The Postman workspace is in `postman/`.
- If you add or change an endpoint, add or update the matching request in the collection so it doesn't go out of date.

## Before opening a PR

- Run `npm run format` (or check with `npm run format:check`)
- Run the backend tests (`npm test` in `backend/`)
- Check the app still runs locally
- Make sure no secrets or `.env` files are included
- Update the README (Setup, Architecture or Known Limitations) if your change affects it
- Update the Postman collection if you touched an endpoint

## Pull requests

1. Push your branch and open a PR into `main`.
2. Fill in the PR template and put the Jira ticket in the PR title, e.g. `A2-12 Edit event form`.
3. At least one other team member needs to review and approve before merging.
4. Throughout the assignment, each reviewer needs to leave at least one actual comment (a question, suggestion or issue) that leads to a fix, not just approvals.
5. Authors: push any fixes from review to the same branch, and reply to the comment saying what you changed.
6. Merge once approved. The branch is deleted automatically after merging.
