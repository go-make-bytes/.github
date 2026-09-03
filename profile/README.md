# go-make-bytes

**Reusable open-source platform services, in Go.** Identity and tokens, EU trust lists,
eID cards, document rendering, audit trails — each service runs on its own, ships as a
container image, and knows nothing about the product that calls it. Products compose
these instead of rebuilding them.

## The services

| Repository | What it is |
|---|---|
| [authbyte](https://github.com/go-make-bytes/authbyte) | The fleet's OAuth 2.0 authorization server — brokers eID logins to one stable person subject and mints DPoP-bound access tokens |
| [trust-anchor](https://github.com/go-make-bytes/trust-anchor) | EU trust-list ingester — fetches the LOTL and national Trusted Lists, verifies their XML signatures and serves versioned trust bundles |
| [web-eid](https://github.com/go-make-bytes/web-eid) | Web eID engine service — validates eID card authentication tokens and runs card-based signing operations behind service authentication |
| [previewbyte](https://github.com/go-make-bytes/previewbyte) | Security-hardened document preview — renders untrusted bytes to inert page images plus text, PDFium in WebAssembly behind hard isolation |
| [eidas-audit](https://github.com/go-make-bytes/eidas-audit) | Append-only, hash-chained signing-evidence sink — consumes signing events from a broker and appends each one tamper-evidently, forever |
| [access-audit](https://github.com/go-make-bytes/access-audit) | GDPR personal-data-access audit sink — every service posts one record per data touch; per-row HMAC seals and purge-safe period checkpoints |

The libraries these services are built from live in
[gmb-lib](https://github.com/gmb-lib), and the open-source qualified electronic
signature platform that composes them is [signbyte](https://github.com/signbyte).

## Run it

Every service publishes a container image at `ghcr.io/go-make-bytes/<name>` — a tag per
release and a tag per commit. **Pin a version tag or a digest, never a moving branch
tag.** Each service's README documents its configuration, its HTTP surface and where it
sits in a deployment.

## Licence, contributing, security

**MIT**, with one deliberate exception: **`authbyte` is AGPL-3.0**, because it is the
identity product itself rather than glue around one. Copyright SIA "Go Make Bytes"
throughout. Issues are welcome on every repository; each carries a `CONTRIBUTING.md`
describing how it is built and tested. Anything exploitable goes through the reporting
route in that repository's `SECURITY.md`, never a public issue.
