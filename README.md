# cert-manager

[![GitLab Sync](https://img.shields.io/badge/gitlab_sync-cert_manager-blue?style=for-the-badge&logo=gitlab)](https://gitlab-internal.spirit-dev.net/github-mirror/helm-cert-manager) <!-- markdownlint-disable MD041 -->
[![GitHub Mirror](https://img.shields.io/badge/github_mirror-cert_manager-blue?style=for-the-badge&logo=github)](https://github.com/spirit-dev/helm-cert-manager)
[![App Status](https://argocd-internal.spirit-dev.net/api/badge?name=cert-manager-turingpi&revision=true&showAppName=true)](https://argocd-internal.spirit-dev.net/applications/cert-manager-turingpi)

<!--TOC-->

- [Installation process](#installation-process)
- [Run Book](#run-book)
  - [`SEC_ERROR_EXPIRED_CERTIFICATE` Certificate seen expired by browsers](#sec_error_expired_certificate-certificate-seen-expired-by-browsers)

<!--TOC-->

## Installation process

The installation is entirely managed by Argocd.

A `Makefile` is present here to ease the first and one-time deployment or in case of an issue.
The installation should be done in two steps:

```shell
#> make dry-run ENV=<ENV>
#> make install ENV=<ENV>
```

## Run Book

### `SEC_ERROR_EXPIRED_CERTIFICATE` Certificate seen expired by browsers

A browser might see, in some rare event a certificate as expired it will be triggering a `SEC_ERROR_EXPIRED_CERTIFICATE` error.
In that scenario, the following action can be taken:

- delete the `secret` related to the certificate, for example: `transmission-test-external-private-tls`
- delete the `CertificateRequest` related to the certificate, for example: `transmission-external-private-tls-6s9tj`
- This will have as an effect to force a new certificate validation.

The root cause of it is most likely a glitch where a certificate is not rotated correctly by `cert manager`
