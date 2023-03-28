# example-bad-repo-packages

This is a misconfigured repository to show how to modify a GitHub Package using write permission or GitHub Actions.

Reposiroty configuration:
- `main` has branch protection enabled with a review from `CODEOWNERS`
- anyone in PagoPA GitHub Organization has `write` permission on this repository
- `packages` inherit access from source repository
- repository package is a docker image
- GitHub Actions has access to `packages`

You can check `packages` settings here https://github.com/orgs/pagopa/packages/container/example-bad-repo-packages/settings

Attack scenario #1:
- a user with `write` permission can modify an existing docker image tagged `v2` in `packages` using his personal PAT token

```sh
docker login ghcr.io
> insert GITHUB_USERNAME
> insert GITHUB_PAT_TOKEN
docker build -f Dockerfile.evil  -t ghcr.io/pagopa/example-bad-repo-packages:v2 .
docker image push ghcr.io/pagopa/example-bad-repo-packages:v2
```

Attack scenario #2:
- a user with `write` permission can modify an existing docker image tagged `v2` in `packages` creating a Pull Request (example Pull Request https://github.com/pagopa/example-bad-repo-packages/pull/1)

## How to configure the GitHub Packages safetly?

See this example https://github.com/pagopa/example-good-repo-packages
