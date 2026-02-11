# Intent Architecture

High-level architecture overview.

## Components

- **Intent Server** - Rust backend (private)
- **Clients** - Desktop (Tauri), Web, Mobile
- **Protocol** - Open specification for third-party clients
- **Bot SDKs** - intent.js and intent.py for bot development

## Client ↔ Server Communication

```
┌─────────────┐
│ Clients │ Desktop, Web, Mobile
└─────────────┘
  ↓
┌─────────────┐
│ Gateway │ WebSocket + MessagePack
└─────────────┘
  ↓
┌─────────────┐
│ Server │ REST API + WebRTC SFU
└─────────────┘
```

See [intent-protocol](https://github.com/IntentAi/intent-protocol) for detailed specs.
