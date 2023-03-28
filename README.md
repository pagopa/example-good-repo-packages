# example-good-repo-packages

This is a well repository to show how to modify a GitHub Package using write permission or GitHub Actions.

Reposiroty configuration:
- `main` has branch protection enabled with a review from `CODEOWNERS`
- anyone in PagoPA GitHub Organization has `write` permission on this repository
- repository package is a docker image
- `packages` doesn't inherit access from source repository
- repository admins has `write` permission on the `packages`
- GitHub Actions has no access to `packages`
- a GitHub Bot has a `write` permission on this repository. We use a secret `GITHUB_BOT_TOKEN` to authenticate the bot with a personal access token. The secret is configured as described here https://github.com/orgs/pagopa/example-good-repo-secrets

You can check `packages` settings here https://github.com/orgs/pagopa/packages/container/example-good-repo-packages/settings

Safe scenario #1:
- a user with `write` permission try to modify an existing docker image tagged `v2` in `packages` using his personal PAT token.
The push operation fails becasuse the user doesn't have `write` permission on `packages`.

```sh
docker login ghcr.io
> insert GITHUB_USERNAME
> insert GITHUB_PAT_TOKEN
docker build -f Dockerfile.evil  -t ghcr.io/pagopa/example-bad-repo-packages:v2 .
docker image push ghcr.io/pagopa/example-bad-repo-packages:v2
```

Safe scenario #2:
- a user with `write` permission create a Pull Request to try get `GITHUB_BOT_TOKEN` value. The GitHub Action fails to start because only a protected branch can use `prod` environment (example Pull Request https://github.com/pagopa/example-good-repo-packages/pull/1)

## How to modify unsecure GitHub Packages?

See this example https://github.com/pagopa/example-good-repo-packages
