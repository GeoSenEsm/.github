# GeoSenEsm — organization documentation

This repository (`GeoSenEsm/.github`) holds organization-level GitHub
configuration and documentation for the GeoSenEsm platform. It is not an
application codebase.


|                |                                                                   |
| -------------- | ----------------------------------------------------------------- |
| Default branch | `main`                                                            |
| Role           | Org profile, shared docs, release notes at the organization level |
| Product repos  | `survey-api`, `survey-admin-panel`, `mobile-app`, `devops`        |


---

## Repository contents


| Path                                       | Purpose                                                     |
| ------------------------------------------ | ----------------------------------------------------------- |
| `README.md`                                | This file — org overview for developers                     |
| `profile/README.md`                        | GitHub organization profile (rendered on the org home page) |
| `profile/GeoSenEsm__User_Guide.pdf`        | End-user / administrator guide                              |
| `profile/GeoSenEsm__User_Guide_v1.0.0.pdf` | Versioned user-guide snapshot                               |
| `profile/geosenesm.png`                    | Branding asset for the org profile                          |
| `LICENSE`                                  | License for materials in this repository                    |


```
.github/   (cloned locally as githubDocs/)
├── README.md
├── LICENSE
└── profile/
    ├── README.md                      # org landing page content
    ├── GeoSenEsm__User_Guide.pdf
    ├── GeoSenEsm__User_Guide_v1.0.0.pdf
    └── geosenesm.png
```

---

## Product repositories


| Repository                                                                      | Default branch | Role                                                                                                      |
| ------------------------------------------------------------------------------- | -------------- | --------------------------------------------------------------------------------------------------------- |
| [GeoSenEsm/survey-api](https://github.com/GeoSenEsm/survey-api)                 | `master`       | Spring Boot REST API (Java 17). Primary SQL Server + MongoDB response documents.                          |
| [GeoSenEsm/survey-admin-panel](https://github.com/GeoSenEsm/survey-admin-panel) | `master`       | Angular 17 admin portal for researchers.                                                                  |
| [GeoSenEsm/mobile-app](https://github.com/GeoSenEsm/mobile-app)                 | `master`       | Flutter respondent app (Android / iOS), white-label `geosenesm` / `urbeat`.                               |
| [GeoSenEsm/devops](https://github.com/GeoSenEsm/devops)                         | `master`       | Ubuntu production setup: Nginx, TLS, privacy policy, Docker Compose (API + admin + MongoDB; SQL Server optional in-compose). |


The three application repositories share one REST contract. Changes that
alter HTTP shape, DTOs, or auth must be coordinated across
`survey-api`, `survey-admin-panel`, and `mobile-app`.

`devops` is deployment documentation only — it does not contain application
source. It tells operators how to run published GHCR images
(`ghcr.io/geosenesm/survey-api:prod`,
`ghcr.io/geosenesm/survey-admin-panel:prod`) behind Nginx on Ubuntu, with
two SQL Server layouts (MongoDB runs in Docker on the app host in both):

| Variant | When to use |
| ------- | ----------- |
| [`variants/separate_mssql`](https://github.com/GeoSenEsm/devops/tree/master/variants/separate_mssql) | App server + separate MSSQL host; Mongo in Compose |
| [`variants/no_separate_mssql`](https://github.com/GeoSenEsm/devops/tree/master/variants/no_separate_mssql) | Single server; MSSQL + Mongo in Docker on the same VM |

Typical host mapping after setup: public `api.*` → local `8083`, public
`admin.*` → local `8084`. Privacy-policy HTML is served from
`/var/www/html/privacy-policy` for the mobile app’s first-login consent flow.

---

## Tags and releases

Prefer annotated tags for releases (for example `v1.0.0`, `v2.0.0`).
Check each product repository for the tags currently published.

---

## CI/CD and container images

CI workflows live under `.github/workflows/` in each **application**
repository (`survey-api`, `survey-admin-panel`, `mobile-app`) — not in this
org docs repo and not in `devops`. Pipelines typically run against the
default branch, build container images, and publish them to the organization
container registry (for example GHCR / GitHub Packages).

Consult the workflow files in `survey-api` and `survey-admin-panel` for the
exact registry, image names, and tag strategy. Use
[GeoSenEsm/devops](https://github.com/GeoSenEsm/devops) for how those
published images are deployed on a production Ubuntu host.

---

## Related documentation

- User guide (PDF): [profile/GeoSenEsm__User_Guide.pdf](profile/GeoSenEsm__User_Guide.pdf)
- Org profile content: [profile/README.md](profile/README.md)
- Per-repo developer notes: README in each of `survey-api`,
  `survey-admin-panel`, and `mobile-app`
- Production server setup: [GeoSenEsm/devops](https://github.com/GeoSenEsm/devops) README and `variants/`
