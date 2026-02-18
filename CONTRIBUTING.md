# Contributing to Intent

Thanks for considering contributing to Intent.

## What We're Building

Intent is an open-source, privacy-first communication platform. Discord without surveillance, resource bloat, and closed-source opacity.

## Project Structure

Intent is split into multiple repositories. Contribute to the one that matches your interest:

| Repository | Purpose | Languages |
|------------|---------|-----------|
| [intent](https://github.com/IntentAi/intent) | Project hub, documentation | Markdown |
| [intent-protocol](https://github.com/IntentAi/intent-protocol) | Protocol specification | Documentation |
| [intent-clients](https://github.com/IntentAi/intent-clients) | Desktop, web, mobile clients | Rust (Tauri), JS/TS, Swift, Kotlin |
| [intent.js](https://github.com/IntentAi/intent.js) | JavaScript bot SDK | TypeScript |
| [intent.py](https://github.com/IntentAi/intent.py) | Python bot SDK | Python |
| [intent-migrate](https://github.com/IntentAi/intent-migrate) | Discord migration tools | TypeScript, Python |

## Development Workflow

**Branches:**
- `main` - production-ready code
- `dev` - integration branch (where applicable)
- `phase` - feature branch

**Work process:**
1. Find or create a GitHub issue
2. Fork the relevant repo
3. Create a branch: `feature/brief-description` or `fix/brief-description`
4. Do the work
5. Open a PR to `dev` (or `phase` if the repo has one)
6. Pass CI and review

## Code Standards

**Optimization first.** Write efficient code. Remove dead code immediately.

**No unnecessary abstractions.** Don't build for hypothetical future requirements.

**Comments explain why, not what.** Code should be self-documenting.

**Tests are required.** Features need tests. Bug fixes need regression tests.

**Security matters.** No buffer overflows, SQL injection, XSS, command injection.

## What We Need

**Phase 1 priorities:**
- Desktop client (Tauri + lightweight UI)
- Web client
- Bot SDKs (intent.js and intent.py)
- Discord migration tools
- Protocol documentation
- MLS E2EE implementation for DMs

## How to Contribute

**If you're new:**
1. Read this guide
2. Check issue trackers for `good-first-issue` tags
3. Join discussions on issues
4. Ask questions if unclear

**Before starting significant work:**
- Comment on the issue to claim it
- For large features, discuss approach first
- Make sure it aligns with project goals

**When submitting a PR:**
- Link to the issue
- Include test coverage
- Run tests locally first
- Sign commits with GPG
- Write clear commit messages: `{type}: {description}`
- No co-authored commits

**PR review process:**
- Code must pass CI
- No decrease in test coverage
- Security implications addressed
- At least one maintainer approval

## Communication

**Issues** - Bug reports, feature requests, task tracking

**Pull requests** - Code review

**Discussions** - Questions, architecture debates, project direction

## Performance Budgets

| Metric | Budget |
|--------|--------|
| Client idle RAM | <80MB |
| Client active voice RAM | <150MB |
| Message send latency | <10ms p95 |
| Voice round-trip latency | <100ms p95 |
| WebSocket event delivery | <5ms p95 |

## What We Don't Accept

- Code that violates performance budgets
- Features that enable surveillance
- Unnecessarily complex solutions
- PRs without corresponding issues
- Code without tests
- Unsigned commits

## License

By contributing, you agree that your contributions will be licensed under the MIT License (for clients/SDKs) or as specified in each repository.

## Final Notes

This project exists because people deserve better than being surveilled for profit. We're building something that respects privacy, system resources, and user freedom.

If you're on board with that, welcome. Let's build something that matters.
