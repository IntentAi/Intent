# Intent Architecture

## Overview

Intent is a privacy-first communication platform split across multiple repositories. The server backend is proprietary; clients, SDKs, and the protocol spec are open source under MIT.

## Components

```
                    ┌──────────────────────────────────────┐
                    │            Intent Server              │
                    │  (Rust, private, proprietary)         │
                    │                                      │
                    │  REST API ─── PostgreSQL              │
                    │  Gateway  ─── Redis Streams           │
                    │  WebRTC SFU ─ Coturn (TURN)           │
                    └────────┬────────────┬────────────────┘
                             │            │
                    HTTP/REST│   WebSocket│(MessagePack)
                             │            │
          ┌──────────────────┴────────────┴──────────────────┐
          │                                                  │
    ┌─────┴──────┐    ┌──────────┐    ┌──────────┐    ┌─────┴──────┐
    │ Web Client │    │ Desktop  │    │ intent.js│    │ intent.py  │
    │ React/TS   │    │ Tauri    │    │ Bot SDK  │    │ Bot SDK    │
    │ (working)  │    │(planned) │    │ (partial)│    │ (partial)  │
    └────────────┘    └──────────┘    └──────────┘    └────────────┘
```

## Web Client

**Repo:** [intent-clients](https://github.com/IntentAi/intent-clients) | **Status:** Working

React 19 + TypeScript + Vite SPA. Communicates with the server via REST for actions and WebSocket for real-time events.

- Three-panel layout: servers, channels, messages
- MessagePack binary encoding over WebSocket
- Zustand for state management
- Gateway opcodes: IDENTIFY, READY, DISPATCH, HEARTBEAT, HEARTBEAT_ACK
- Events: MESSAGE_CREATE, MESSAGE_UPDATE, MESSAGE_DELETE, SERVER_CREATE, CHANNEL_CREATE
- Tailwind CSS styling

## Protocol Specification

**Repo:** [intent-protocol](https://github.com/IntentAi/intent-protocol) | **Status:** Near-complete

The protocol spec defines everything a third-party client or bot needs to interact with Intent.

- **REST API** — Endpoints for servers, channels, messages. Snowflake IDs, cursor-based pagination, typed error responses.
- **Gateway** — WebSocket with MessagePack binary frames. 13 opcodes (0-12), 14 event types. Heartbeat keepalive, sequence numbers for resume.
- **Voice** — WebRTC SFU architecture. SDP offer/answer via gateway opcode 12. ICE/DTLS-SRTP transport. Opus codec at 32-128 kbps adaptive. Speaking detection via RFC 6464 audio levels.
- **Encryption** — MLS (RFC 9420) for E2EE DMs. X25519 DHKEM, AES-128-GCM, Ed25519 signatures. Key package management, multi-device support.
- **Discord Mapping** — Endpoint, event, and object field mapping between Intent and Discord APIs.

## Bot SDKs

### intent.py

**Repo:** [intent.py](https://github.com/IntentAi/intent.py) | **Status:** Core library working, bot framework stubbed

- Gateway client with MessagePack, heartbeat, exponential backoff reconnection
- REST client with per-route rate limiting and all Phase 1 endpoints
- Data models: User, Server, Channel, Message
- 56+ tests passing
- Mirrors discord.py patterns
- Missing: Client/Bot class, command decorator framework, event system

### intent.js

**Repo:** [intent.js](https://github.com/IntentAi/intent.js) | **Status:** REST working, gateway not started

- REST client with rate limiting, retry logic, typed errors
- All Phase 1 endpoints (servers, channels, messages CRUD)
- Dual ESM/CJS build via tsup
- Mirrors discord.js patterns
- Missing: Gateway/WebSocket client, Client class, structure classes, event system

## Migration Toolkit

**Repo:** [intent-migrate](https://github.com/IntentAi/intent-migrate) | **Status:** Design documented, implementation not started

Four components planned:
1. **Webhook compatibility** — Accept Discord webhook format on Intent endpoints
2. **Server exporter** — Discord bot that exports server structure to JSON
3. **Server importer** — CLI that recreates structure on Intent from the export
4. **Bridge bot** — Bidirectional message forwarding between Discord and Intent during transition

## Communication Flow

**REST API** handles stateless operations: auth, CRUD for servers/channels/messages, role management, invites.

**WebSocket Gateway** handles real-time: event dispatch, heartbeat keepalive, voice signaling. Uses MessagePack binary encoding. Clients authenticate with opcode 2 (Identify), receive initial state via opcode 3 (Ready), then receive events via opcode 0 (Dispatch).

**Voice** uses WebRTC through the gateway for signaling. Clients send opcode 4 to join a voice channel, receive connection details via VOICE_SERVER_UPDATE event, then exchange SDP/ICE via opcode 12. Audio flows over UDP with DTLS-SRTP encryption.
