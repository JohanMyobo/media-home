# Media Home

Personal media library and playback platform designed to work with cloud storage today and a self-hosted NAS tomorrow.

## Product

The end-user product is **JojoFlix**. `Media Home` is the technical/development project name.

Build a clean, reusable **personal cinema platform** instead of depending on the limited playback experience of a cloud-storage app.

JojoFlix is intended to be shared with colocataires and friends through individual accounts, while keeping the storage layer replaceable.

```text
Cloud storage
      │
      ▼
 Media server
      │
      ▼
 Media library
      │
 ┌────┴────┐
 ▼         ▼
Browser  Native player
      │
      ▼
   Devices

Future:
NAS ────────► same media server / same interface
```

## Initial direction

- Evaluate a practical cloud provider to replace TeraBox.
- Use **Jellyfin** as the media-server foundation where appropriate.
- Keep the storage abstraction independent from the UI.
- Support individual users with independent playback progress.
- Design for secure remote access from the beginning.
- Use an existing high-quality player such as Infuse when it provides a better playback experience.
- Build a custom interface only where it adds real value.
- Design the system so migration to the future NAS does not require rebuilding the product.
- The final hosted service must continue working when the Mac mini is powered off.

## POC progress

### Phase 1 — Local playback baseline: **validated**

The first local POC is running on a **Mac mini M4 over Ethernet**.

Validated:

- Jellyfin installed and operational.
- `Films` library created from `/Users/johandhos/Desktop/Media Home/Movies`.
- Multiple MKV movies indexed with posters and metadata.
- 4K HEVC/H.265 playback works.
- Individual user accounts work.
- Playback position is stored independently per user.
- A second device on the local network can connect to Jellyfin and resume playback.
- Two simultaneous 4K streams work on the local network.
- Direct streaming works for compatible HEVC/AAC files.
- Transcoding works when the browser cannot directly play the source; the Mac mini M4 handled the tested 4K transcode in real time.

Tested examples:

- `Projet Dernière Chance` — 4K HEVC Main 10, AAC — **Direct Streaming**.
- `Gladiator` — 4K HEVC Main 10, AAC, HDR10 — **Direct Streaming**.
- `Troie` — 4K HEVC Main 10, AC3, HDR10 — **Transcoding to H.264/AAC** in the tested browser.
- Two simultaneous streams were tested successfully: one direct stream and one transcode.

### Next phase

1. Choose the cloud storage backend.
2. Connect cloud storage to the media-server layer.
3. Validate remote playback and HTTPS access.
4. Document the cloud → server → player architecture.
5. Start the first JojoFlix interface on top of the validated playback layer.
6. Later move the server to a VPS so JojoFlix remains available when the Mac mini is off.

## POC goals

1. Establish a reliable local Jellyfin playback baseline. **Done.**
2. Select the best cloud-storage backend for the project.
3. Connect a small test movie library.
4. Confirm reliable direct/streamed playback and transcoding when necessary. **Local baseline done.**
5. Validate subtitles, metadata, resume position and common formats. **Core local tests done.**
6. Validate multiple individual users. **Done.**
7. Validate secure remote access over HTTPS.
8. Establish the architecture for the future NAS and VPS.
9. Build the first version of the JojoFlix personal cinema UI.

## Architecture principles

- **Storage-agnostic:** cloud today, NAS tomorrow.
- **Playback-first:** prioritize reliable playback over unnecessary custom features.
- **Multi-user:** each person gets their own account and playback state.
- **Secure by default:** remote access uses HTTPS and a controlled entry point.
- **Self-hostable:** the final system should be comfortable running locally.
- **Portable:** avoid locking the application to a single storage provider.
- **Incremental:** every POC step should remain useful for the final system.

## POC documentation

- [`docs/POC-01.md`](docs/POC-01.md) — shared personal cinema POC and acceptance criteria.

## Project status

**Phase 1 complete — Local playback baseline validated.**

**Next:** compare cloud-storage backends and prepare the cloud/server architecture. The long-term target is a VPS-hosted JojoFlix instance backed by replaceable cloud storage, with a future NAS migration path.
