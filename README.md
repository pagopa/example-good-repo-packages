# example-bad-repo-secrets

This is a misconfigured repository to show how to leak Repository Secrets using GitHub Actions.

In this repository is configured is a secret named `UNSECURE_SECRET`.

Using GitHub Action you can get the secret (catch the flag).

Scenario:
- `main` has branch protection enabled
- anyone in PagoPA GitHub Organization has `write` permission on this repository

Attack scenario:
- an internal user with `write` permission create a Pull Request to get `UNSECURE_SECRET` value (example Pull Request https://github.com/pagopa/example-bad-repo-secrets/pull/1)
