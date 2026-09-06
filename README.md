# Media Home

Personal media library and playback platform designed to work with cloud storage today and a self-hosted NAS tomorrow.

## Vision

Build a clean, reusable **personal cinema platform** instead of depending on the limited playback experience of a cloud-storage app.

Media Home is intended to be shareable with colocataires and friends through individual accounts, while keeping the storage layer replaceable.

```text
Cloud storage (POC)
        │
        ▼
   Media server
        │
        ▼
   Media library
        │
   ┌────┴────┐
   ▼         ▼
 Browser   Native player
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

## POC goals

1. Establish a reliable local Jellyfin playback baseline.
2. Select the best cloud-storage backend for the project.
3. Connect a small test movie library.
4. Confirm reliable direct/streamed playback and transcoding when necessary.
5. Validate subtitles, metadata, resume position and common formats.
6. Validate multiple individual users.
7. Validate secure remote access over HTTPS.
8. Establish the architecture for the future NAS.
9. Build the first version of the personal cinema UI.

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

**Phase 1 — Local playback baseline**

Next: validate Jellyfin locally, then introduce the cloud storage layer and remote access.
