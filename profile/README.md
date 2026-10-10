# Codex Remote

**Use your phone as a remote workbench for Codex running on your Mac.**

[Product home](https://github.com/codex-remote/codex-remote) |
[Quick start](https://github.com/codex-remote/codex-remote#quick-start) |
[Source code](https://github.com/codex-remote/codex-remote#source-code) |
[Roadmap](https://github.com/codex-remote/codex-remote/blob/main/ROADMAP.md) |
[Releases](https://github.com/codex-remote/homebrew-tap/releases)

![Codex Remote product preview](https://raw.githubusercontent.com/codex-remote/codex-remote/main/assets/social-preview-v2.png)

Codex Remote is an independent open-source project. It is not affiliated with
or endorsed by OpenAI. Codex and OpenAI are trademarks of their respective
owners.

> [!WARNING]
> Codex Remote is pre-release software. The current public Beta is for Apple
> Silicon Macs and iPhone Safari. Use the same trusted Wi-Fi nearby, or a
> private Tailscale network when away. It is unsigned, not Apple notarized,
> and must not be exposed directly to the public internet.

## Try the current Beta

```bash
brew trust --formula codex-remote/tap/codex-remote
brew install codex-remote/tap/codex-remote
codex-remote setup --workspace-root ~/work
codex-remote pair
```

For private remote access, install Tailscale on the Mac and iPhone, sign in to
the same Personal tailnet, and follow the [remote access guide](https://github.com/codex-remote/codex-remote/blob/main/docs/private-remote-access.md).

The terminal displays a one-time QR code. Scan it with iPhone Safari, choose a
project and session, and continue working while Codex and project files stay on
your Mac. Read the [security and network limitations](https://github.com/codex-remote/codex-remote#requirements)
before installing.

## Architecture

```mermaid
flowchart LR
    Phone["iPhone App / Mobile Web"] --> Gateway["Mobile Web Gateway"]
    Gateway --> Relay["Relay + Run Server"]
    Relay --> Agent["Mac Agent"]
    Agent --> Codex["Codex App Server"]
    Relay --> Runtime[("PostgreSQL + Valkey")]
    Admin["Admin Platform"] -. diagnostics .-> Relay
    Distribution["Runtime Distribution"] --> Gateway
    Distribution --> Relay
    Distribution --> Agent
    Tap["Homebrew Tap"] --> Distribution
```

The project intentionally uses independent repositories. Cross-repository
integration happens through versioned HTTP, SSE, WebSocket, schema, fixture,
and release-manifest contracts rather than shared source imports.

## Repositories

| Repository | Responsibility |
| --- | --- |
| [iphone-app](https://github.com/codex-remote/iphone-app) | Native SwiftUI iPhone client |
| [mobile-web](https://github.com/codex-remote/mobile-web) | React client and same-origin Gateway |
| [relay-server](https://github.com/codex-remote/relay-server) | Relay, Run Server, Runtime Auth, and contracts |
| [mac-agent](https://github.com/codex-remote/mac-agent) | Local Codex execution and workspace adapter |
| [admin-platform](https://github.com/codex-remote/admin-platform) | Diagnostics server, collector, and admin UI |
| [runtime-distribution](https://github.com/codex-remote/runtime-distribution) | Runtime CLI, supervisor, assembly, and release checks |
| [codex-remote](https://github.com/codex-remote/codex-remote) | Product home, quick start, screenshots, source map, and roadmap |
| [homebrew-tap](https://github.com/codex-remote/homebrew-tap) | Homebrew installation and public Runtime releases |
| [docs](https://github.com/codex-remote/docs) | Product, architecture, protocol, ADR, and release documentation |

## Contributing and security

Start with [CONTRIBUTING.md](../CONTRIBUTING.md) and open changes in the
repository that owns the affected component. Report vulnerabilities privately
as described in [SECURITY.md](../SECURITY.md).

All current source repositories are licensed under the
[Apache License 2.0](../LICENSE). Previously published Beta archives retain the
license embedded in those immutable artifacts.
