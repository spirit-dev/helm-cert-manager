# Welcome to cert-manager

[![App Status](https://argocd-internal.spirit-dev.net/api/badge?name=cert-manager-turingpi&revision=true&showAppName=true)](https://argocd-internal.spirit-dev.net/applications/cert-manager-turingpi)

## Table of content

[[_TOC_]]

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
