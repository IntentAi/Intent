# Changelog

All notable changes to Intent will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [Unreleased]

### Project Restructure

- Split monorepo into multiple repositories:
 - Server backend: Private (proprietary)
 - Clients, SDKs, protocol: Public (MIT)
- Created IntentAi GitHub organization for public repos
- Established clear separation between server (proprietary) and clients (open source)

### Added (from previous development)

- REST API for servers, channels, messages, and roles
- User authentication with argon2 password hashing
- Session management with Redis (7-day TTL, auto-refresh)
- Permission system with bitfield checks and Redis caching
- WebSocket gateway for real-time events
- Binary MessagePack protocol for efficient communication
- Database schema with Snowflake IDs for messages
- HELLO/IDENTIFY/READY WebSocket handshake
- Heartbeat mechanism for connection monitoring
- Redis Streams for event distribution
- Voice service foundation (WebRTC SFU in progress)

### Technical

- Rust backend with Axum framework
- PostgreSQL database with SQLx
- Redis for sessions, caching, and event streams
- JWT-based authentication
- Atomic ownership checks
- N+1 query optimization in permission resolver

## Phase 1 Roadmap (In Progress)

- Voice WebRTC SFU completion
- MLS end-to-end encryption for DMs
- Tauri desktop client
- Web client
- Docker image distribution
- CI/CD pipeline
- Bot API and webhooks
- Observability (metrics and logging)

## Phase 2 Roadmap

See [intent-clients](https://github.com/IntentAi/intent-clients) for client roadmap.

## Phase 3 Roadmap

See individual repo roadmaps for ecosystem features.

---

**Note:** Intent is in early active development. This changelog tracks major milestones across all repositories.
