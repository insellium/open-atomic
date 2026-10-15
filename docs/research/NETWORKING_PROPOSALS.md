# Online Multiplayer — Proposals for a Later Decision

Status: discussion. Multiplayer implementation is planned after faithful local gameplay and the content system. This document does not select a network architecture.

## Ceotom's proposal

- One player's machine runs the authoritative match simulation.
- Clients connect directly to the host over UDP when possible.
- A server helps players find one another, create public or code-based lobbies, discover addresses, and exchange ICE/STUN candidates.
- If a direct path is unavailable, traffic uses a relay. Proposed relay transports are WebTransport, with WebSocket as a fallback.
- Match discovery may use a browser interface while the game client remains native.

## Existing approaches in the projects under review

- Egerion: deterministic simulation on each peer, rollback, and a host that forwards inputs; includes lobbies, direct UDP, and a relay. The host configures the match but is not the sole owner of game state. See `Egerion - open-atomic-bomberman-97-main/docs/adr/0011-online-multiplayer-architecture.md`.
- elraro: a client-server model in which the server runs the match; its description also mentions client-side prediction of local actions. See `elraro - atomic-bomberman-main/README.md` and that project's `docs/specifications/networking.md`.
- Boom Buds: deterministic peer simulation and rollback over WebRTC. See `mayerwin - Boom-Buds-main/src/net/rollback.ts`.

## Questions to resolve later

1. **Game-state authority:** a single host or deterministic state on every peer. This is a separate choice from ICE, STUN, lobbies, and transport.
2. **Latency and loss:** measure control responsiveness, visible corrections, match stalls, and desynchronization with 2–10 players.
3. **Host departure:** end the match, transfer the role, or use another mechanism.
4. **Relay:** assess availability, latency, cost, and complexity of UDP, WebTransport, and WebSocket for the target native platforms.
5. **Content and audio:** agree on installed stage/skin versions and hashes, including each stage's music and any skin-specific audio replacements, and quickly send the small text `.SCH` before a match. Shared default audio is part of the base game or a separately identified package; skins without overrides use it without copying files. Player-owned sound events carry the source player ID so every client resolves the event using **that player's equipped skin**, even in a match mixing several skins and the standard bomber. For a randomized voice event, synchronize the chosen clip identity or an equivalent presentation-only seed so clients hear the same line without consuming gameplay simulation randomness. Each client's voice mute setting affects only local playback. If random trampolines from `extra.ini` are allowed online, all participants need the same placement. Handle original game materials separately.
6. **Trust and protection:** decide who may change state, what clients validate, and how incompatible builds are handled.

## Selection criterion

Choose after working prototypes have run the same scenarios: direct connections and relays, latency and packet loss, several players, a low-end client, and player or host departure. Record results and limitations. No existing project wins by default.
