# Brew v0.1.0

**Initial release** — the first public build of Brew, the CI/CD orchestrator for CiderStack macOS infrastructure.

## Highlights

- **Single binary deployment** — Download, extract, run. Brew ships as a compiled binary with a built-in web dashboard. No runtime dependencies, no external databases.
- **Ephemeral GitHub Actions runners** — Create pools of self-hosted macOS runners that auto-register with GitHub, execute one job in a clean VM, and tear themselves down.
- **Fleet-wide VM management** — Pair Mac nodes with cryptographic handshake, monitor health in real time, and manage VMs (clone, snapshot, restore, execute commands) from one place.
- **Job scheduling** — Submit CI/CD jobs via API or GitHub webhooks. Brew assigns each job to the best available node based on CPU, memory, and Apple Silicon chip type.
- **Persistent VM pools** — Keep template VMs pre-cloned and ready to go. Pools auto-replenish as VMs are consumed, with configurable TTL for recycling.

## What's included

- Web dashboard with setup wizard, node pairing, VM browser, job queue, and runner pool management
- REST API for all operations (nodes, VMs, jobs, pools, runner pools, templates, alerts)
- Prometheus metrics endpoint (`/api/metrics`) for Grafana integration
- GitHub webhook handler with HMAC-SHA256 verification for push and pull request events
- Slack notifications for job status and node health alerts
- TypeScript/JavaScript SDK (`@ciderstack/fleet-sdk`)
- Trigger configs for automated job dispatch on push/PR events

## Downloads

| Platform | Architecture | Download |
|---|---|---|
| macOS | Apple Silicon (arm64) | [brew-v0.1.0-darwin-arm64.tar.gz](https://github.com/ciderstack/Brew/releases/download/v0.1.0/brew-v0.1.0-darwin-arm64.tar.gz) |
| macOS | Intel (x64) | [brew-v0.1.0-darwin-x64.tar.gz](https://github.com/ciderstack/Brew/releases/download/v0.1.0/brew-v0.1.0-darwin-x64.tar.gz) |
| Linux | x86_64 | [brew-v0.1.0-linux-x64.tar.gz](https://github.com/ciderstack/Brew/releases/download/v0.1.0/brew-v0.1.0-linux-x64.tar.gz) |
| Linux | ARM64 | [brew-v0.1.0-linux-arm64.tar.gz](https://github.com/ciderstack/Brew/releases/download/v0.1.0/brew-v0.1.0-linux-arm64.tar.gz) |

## Getting started

```bash
tar xzf brew-v0.1.0-darwin-arm64.tar.gz
cd brew-v0.1.0-darwin-arm64
./brew
```

Open [http://localhost:8470](http://localhost:8470) to create your admin account and pair your first node.

## Requirements

- macOS 13+ or Linux (x64/arm64) for the Brew orchestrator
- macOS nodes running [CiderStack Fleet](https://ciderstack.com) for VM operations
- GitHub PAT with `admin:org` + self-hosted runners scope (for ephemeral runner pools)

## Known limitations

- Max 2 concurrent VMs per Mac (Apple Virtualization framework restriction)
- Build artifact uploads require `BREW_PUBLIC_URL` to be set so VMs can download artifacts
- SQLite database — designed for single-instance deployments
