# Contributing to Codex Remote

Thank you for contributing to Codex Remote. The project is split into
independent repositories so each component can be reviewed, tested, and
released on its own.

## Choose the owning repository

- iPhone behavior and native UI: `iphone-app`
- Browser UI and Gateway behavior: `mobile-web`
- Runtime HTTP/SSE, authentication, Relay, and public contracts: `relay-server`
- Local Codex execution and workspace access: `mac-agent`
- Diagnostics and administration: `admin-platform`
- Runtime packaging and release automation: `runtime-distribution`
- Homebrew metadata and release documentation: `homebrew-tap`
- Architecture, ADRs, and protocol design: `docs`

Do not introduce sibling source imports, submodules, `go.work`, or symlinked
sharing. Coordinate cross-repository work through versioned schemas, fixtures,
compatibility records, and separate commits.

## Before opening a pull request

1. Open or reference an issue for a behavior, protocol, security, or
   cross-repository change.
2. Keep the change focused and update tests, contracts, documentation, and the
   changelog owned by that repository.
3. Run the repository's documented test and build commands.
4. Remove credentials, pairing links, personal paths, workspace content, and
   sensitive diagnostics from commits and screenshots.
5. Sign off every commit with `git commit -s` to certify the
   [Developer Certificate of Origin](https://developercertificate.org/).

Pull requests require passing checks and maintainer review. A contribution is
not accepted until it is merged into the official repository.

## Licensing

Unless explicitly stated otherwise, contributions are submitted under the
Apache License 2.0 and the repository NOTICE. The DCO sign-off confirms that
you have the right to submit the contribution under those terms.
