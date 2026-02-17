# Intent

**Discord is forcing government ID verification to talk to your friends. We're building the alternative.**

## Why Intent Exists

Discord just rolled out mandatory government ID and facial recognition. Your biometric data on their servers. Forever. No opt-out.

Intent exists because your right to private communication shouldn't come with surveillance attached.

## What You Get

- **Actually private**: E2EE for DMs using MLS protocol
- **Actually lightweight**: Sub-80MB RAM idle (Discord: 400MB+)
- **Actually fast**: WebRTC SFU for sub-100ms voice latency
- **Self-hostable**: Run on your own infrastructure
- **Open clients**: Verify privacy claims in the code

**No government IDs. No facial recognition. No surveillance.**

## Project Structure

Intent is split into multiple repositories:

- **[intent](https://github.com/IntentAi/intent)** - This repo (project hub)
- **[intent-protocol](https://github.com/IntentAi/intent-protocol)** - Protocol specification
- **[intent-clients](https://github.com/IntentAi/intent-clients)** - Desktop, web, mobile clients
- **[intent.js](https://github.com/IntentAi/intent.js)** - JavaScript/TypeScript bot SDK
- **[intent.py](https://github.com/IntentAi/intent.py)** - Python bot SDK
- **[intent-migrate](https://github.com/IntentAi/intent-migrate)** - Discord migration toolkit

## Current Status

**Phase 1 MVP — nearing completion.**

### Working

- **Web client** — React 19 + TypeScript SPA with real-time messaging, server/channel management, and auth ([intent-clients](https://github.com/IntentAi/intent-clients))
- **Protocol spec** — REST API, gateway opcodes, events, voice signaling, codec requirements, MLS E2EE spec, and Discord compatibility mapping fully documented ([intent-protocol](https://github.com/IntentAi/intent-protocol))
- **Python bot SDK** — Gateway client, REST client with rate limiting, data models, 56+ passing tests ([intent.py](https://github.com/IntentAi/intent.py))
- **JS/TS bot SDK** — REST client with per-route rate limiting, typed error handling, dual ESM/CJS build ([intent.js](https://github.com/IntentAi/intent.js))

### In Progress

- **Voice** — WebRTC SFU signaling is spec'd, server-side infrastructure partially built, client-side not started
- **Bot frameworks** — Gateway and Client classes not yet wired in either SDK
- **Desktop client** — Tauri wrapper planned, not started

### Planned

- MLS end-to-end encryption for DMs
- Docker image distribution and self-hosting guide
- Discord migration tools (server exporter, importer, bridge bot)
- Mobile clients (iOS, Android)

**Not ready for daily use yet.** Active development.

## Self-Hosting

In development: One-command Docker deployment.

See [docs/self-hosting.md](docs/self-hosting.md) for details.

## How to Contribute

We need you.

**Find your fit:**
- **Frontend**: Web client improvements, Tauri desktop wrapper
- **Voice**: WebRTC client integration, SFU testing
- **Bot SDKs**: Gateway clients, structure classes, command frameworks (intent.js / intent.py)
- **Migration tools**: Discord server exporter, importer, bridge bot
- **Mobile**: Swift (iOS), Kotlin (Android) - Phase 2
- **Docs**: Guides, tutorials, API documentation
- **Testing**: Break things, report bugs

**Start here:**
1. Check [open issues](https://github.com/IntentAi/intent/issues)
2. Read [CONTRIBUTING.md](CONTRIBUTING.md)
3. Pick a repo based on your interest
4. Submit a PR

**Can't code?**
- Star the repos
- Share with communities
- Test releases
- Write documentation

## Architecture

See [docs/architecture.md](docs/architecture.md) for high-level overview.

For technical details, see [intent-protocol](https://github.com/IntentAi/intent-protocol).

## Roadmap

**Phase 1 (MVP):**
Text channels, voice channels, servers with roles/permissions, E2EE DMs, desktop/web clients

**Phase 2 (Community):**
Threads, video calls, screen sharing, custom emoji, moderation tools, mobile apps

**Phase 3 (Ecosystem):**
Plugin system, optional federation, bridges (Discord/Matrix/IRC), positional audio

Full roadmap in [tasks docs](https://github.com/IntentAi/intent/tree/main/tasks%20docs) (in development).

## License

MIT License. Clients and SDKs are open source.

Server backend is proprietary (enables monetization through managed hosting).

See [LICENSE](LICENSE) for details.

---

When the platform you rely on demands government IDs, you have two choices: comply or leave.

We're building the third option: **own it yourself**.

Star the repos. Watch for releases. Contribute if you can.

Discord doesn't get to own private communication. Not anymore.
