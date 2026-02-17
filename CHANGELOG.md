# Changelog

All notable changes to Intent will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [Unreleased]

### Project Restructure

- Split monorepo into multiple repositories
  - Server backend: Private (proprietary)
  - Clients, SDKs, protocol: Public (MIT)
- Created IntentAi GitHub organization for public repos

### intent-clients (Web Client)

- React 19 + TypeScript + Vite single-page application
- Three-panel Discord-style layout (servers, channels, messages)
- Login and registration with token-based auth
- WebSocket gateway client with MessagePack binary encoding
- Real-time messaging with optimistic UI and rollback on error
- Server and channel CRUD with modal creation flows
- Gateway event handling: MESSAGE_CREATE, MESSAGE_UPDATE, MESSAGE_DELETE, SERVER_CREATE, CHANNEL_CREATE
- Heartbeat with exponential backoff reconnection (1-30s with jitter)
- Zustand state management for auth, servers, channels, messages, users
- Message grouping by author, auto-scroll, Shift+Enter for newlines
- Tailwind CSS styling, ESLint + Prettier enforced

### intent-protocol (API Specification)

- REST API spec for servers, channels, messages with full CRUD, error codes, and pagination
- Authentication spec covering token types, permission bitfields, and OAuth2 outline
- Rate limiting spec with per-route buckets and global limits
- Gateway opcodes 0-12 documented with payload structures and examples
- Gateway events (14 total) with schemas, triggers, and ordering guarantees
- Voice signaling spec: WebRTC SFU architecture, opcode 4 and 12 payloads, ICE/DTLS/SRTP lifecycle, STUN/TURN configuration, speaking detection, bitrate adaptation
- Voice codec spec: Opus configuration, SDP negotiation, RTP header extensions, RTCP feedback, encoder profiles
- MLS E2EE spec: Ciphersuite selection, key package management, DM/group DM flows, encrypted message format, multi-device support, threat model
- Discord compatibility mapping: endpoint mapping, event name mapping, object field mapping

### intent.py (Python Bot SDK)

- Gateway client with MessagePack WebSocket, heartbeat, and reconnection logic
- REST client with all Phase 1 endpoints and per-route rate limiting
- Data models for User, Server, Channel, Message with proper type hints
- Typed exception hierarchy (Unauthorized, Forbidden, NotFound, RateLimited, ServerError)
- 56+ passing tests covering gateway, REST, and models

### intent.js (TypeScript Bot SDK)

- REST client with all Phase 1 endpoints (servers, channels, messages CRUD)
- Per-route rate limit buckets with global rate limit handling
- Automatic retry on 5xx with exponential backoff
- 7 typed error classes covering all HTTP status codes
- Snowflake ID validation, 15s request timeout
- Dual ESM/CJS build via tsup with TypeScript declarations

### intent-migrate (Discord Migration Toolkit)

- Migration strategy documented (webhook compat, server import, bridge bot, message import)
- Directory structure and component READMEs in place
- Implementation not yet started

## Still To Do (Phase 1)

- Voice: finish WebRTC SFU audio forwarding, build client-side WebRTC integration
- Bot SDKs: wire up gateway clients and Client/Bot classes in both intent.js and intent.py
- Desktop client: Tauri wrapper around web client
- MLS E2EE: implement encrypted DMs
- Self-hosting: Docker image distribution and deployment guide
- CI/CD pipeline
- Migration tools: build exporter, importer, and bridge bot

## Phase 2 Roadmap

See [intent-clients](https://github.com/IntentAi/intent-clients) for client roadmap.

## Phase 3 Roadmap

See individual repo roadmaps for ecosystem features.

---

**Note:** Intent is in early active development. This changelog tracks major milestones across all repositories.
