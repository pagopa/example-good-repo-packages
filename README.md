# example-bad-repo-secrets

This is a well configured repository to show how to prevent to leak Repository Secrets using GitHub Actions.

In this repository is configured is a secret named `SECURE_SECRET`.

Using GitHub Action you can't get the secret (catch the flag).

Scenario:
- `main` has branch protection enabled
- anyone in PagoPA GitHub Organization has `write` permission on this repository

Attack scenario:
- an internal user with `write` permission create a Pull Request to try get `SECURE_SECRET` value (example Pull Request https://github.com/pagopa/example-good-repo-secrets/pull/1)
