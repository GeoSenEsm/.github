# GeoSenEsm — Repositories overview

This repository (.github) contains organization-level configuration and documentation (User guide) for the GeoSenEsm organization.

## Repositories

- GeoSenEsm/survey-admin-panel
  - Default branch: `master`
  - Notes: Frontend/admin UI for surveys (TypeScript).
    
- GeoSenEsm/survey-api
  - Default branch: `master`
  - Notes: Backend API for surveys (Java).

- GeoSenEsm/mobile-app
  - Default branch: `master`
  - Notes: Mobile application (Dart / Flutter).

- GeoSenEsm/devops
  - Default branch: `main` (a `master` branch also exists)
  - Notes: CI/CD and infra configuration.

## Tags and releases

We generally use annotated tags for releases.

## CI/CD pipelines and container image publishing

- There are CI pipelines configured that run on the `main` branches. These pipelines build container images and publish them to the organization's configured container registry (for example GitHub Container Registry / ghcr.io or GitHub Packages). Check each repository's workflow files in `.github/workflows/` for the exact publishing target and tags.
