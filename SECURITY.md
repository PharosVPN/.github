# Security Policy

PharosVPN is a self-hostable VPN platform. We take security seriously and welcome
coordinated disclosure.

> ⚠️ **PharosVPN is pre-alpha.** It is for experimentation, self-hosting, and code
> review — **not** production privacy or security use. Nothing has been
> independently audited. See the
> [project status](https://github.com/PharosVPN/docs/blob/main/STATUS.md) and the
> [threat model](https://github.com/PharosVPN/docs/blob/main/threat-model.md).

## Reporting a vulnerability

Email **khalefa@alahmad.org** with details and, ideally, a proof of concept.
Please **report privately** and give us reasonable time to fix before any public
disclosure. We aim to acknowledge within a few days.

When reporting, include: the repo + version/commit, the component (controller /
node / relay / client), the impact, and reproduction steps.

## Supported versions

There are **no released versions yet**. Security fixes land on `main` in the
relevant repo. Use the latest `main`; pin a commit if you need stability.

## Scope

**In scope** — issues in PharosVPN's own code/design:
- The controller (`coxswain`): provisioning, PKI/enrollment, account sync, the
  admin API/UI.
- The data/control plane (`node`, `relay`) and the control protocol (mTLS, onion).
- The clients (`caravel-*`) and the shared core (profile parsing, sync, the
  tunnel engine).
- End-to-end profile sealing, key handling, authentication/authorization,
  privilege boundaries, and identity/enrollment trust.

**Out of scope (for now):**
- Vulnerabilities in third-party dependencies — report them upstream. We pin
  versions and track reachable CVEs (see the dependency posture).
- Volumetric DoS — the control plane has no public inbound ports by design.
- The operator's own misconfiguration or compromised infrastructure.
- The **known, documented residual risks** in the
  [threat model](https://github.com/PharosVPN/docs/blob/main/threat-model.md)
  (e.g. guard-relay origin exposure, Fleet-CA server linkage, global-adversary
  traffic correlation). These are tracked design gaps, not new findings — but a
  *new* way to exploit one, or a gap we missed, is in scope.

## Disclosure

We prefer coordinated disclosure. Once a fix is available we'll credit the
reporter (unless you prefer to stay anonymous) and note the issue in the release.
