# GeoSenEsm — Repositories overview

This repository (.github) contains organization-level configuration and documentation for the GeoSenEsm organization. The purpose of this README is to list the primary repositories in this organization, the intended tagged code versions, and where CI/CD pipelines publish built container images.

## Repositories

- GeoSenEsm/survey-admin-panel
  - Default branch: `master`
  - Notes: Frontend/admin UI for surveys (TypeScript).
  - Tagged code versions: target tag `v1.0.0` on `master` (create if missing).

- GeoSenEsm/survey-api
  - Default branch: `master`
  - Notes: Backend API for surveys (Java).
  - Tagged code versions: target tag `v1.0.0` on `master` (create if missing).

- GeoSenEsm/mobile-app
  - Default branch: `master`
  - Notes: Mobile application (Dart / Flutter).
  - Tagged code versions: target tag `v1.0.0` on `master` (create if missing).

- GeoSenEsm/devops
  - Default branch: `main` (a `master` branch also exists)
  - Notes: CI/CD and infra configuration.
  - Tagged code versions: target tag `v1.0.0` on `master` (creates a release for the infra state). If you prefer tagging `main` instead, update this README accordingly.

## Tags and releases

We generally use annotated tags for releases. The current organization-wide target release tag is `v1.0.0`. If the tag does not already exist in a repository, you can create it with the following commands (run locally with an authenticated `gh` and `git`):

Create an annotated tag at the tip of `master` and push it:

```bash
# Example for repo OWNER/REPO
git fetch origin
git checkout master
git pull origin master
git tag -a v1.0.0 -m "v1.0.0"
git push origin v1.0.0
```

Or use GitHub CLI to create a release (creates an annotated tag on GitHub):

```bash
gh release create v1.0.0 --repo GeoSenEsm/REPO --target master --title "v1.0.0" --notes "Release v1.0.0"
```

If your repo uses `main` as default (like `devops`) but you need `master` to be tagged, ensure the `master` branch exists and points at the intended commit.

## CI/CD pipelines and container image publishing

- There are CI pipelines configured that run on the `test` and `main` branches. These pipelines build container images and publish them to the organization's configured container registry (for example GitHub Container Registry / ghcr.io or GitHub Packages). Check each repository's workflow files in `.github/workflows/` for the exact publishing target and tags.

- Note: changing the default branch (for example switching `devops` from `main` to `master`) can affect pipeline triggers and branch protection rules. Update any workflow filters and branch protection settings as needed.

## Next steps / recommendations

- Verify that `v1.0.0` exists where you expect it. Use `git ls-remote --tags origin | grep "refs/tags/v1.0.0"` or `gh release view v1.0.0 --repo OWNER/REPO`.
- If you want, use a small script to create `v1.0.0` across multiple repos and optionally set `devops` default branch to `master` — this repo's root contains organization-level docs and is a good place to keep that script.

If you want, I can add that script to this repository or open a PR creating/adjusting the README text further.
