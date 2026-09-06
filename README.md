# Media Home

Personal media library and playback platform designed to work with cloud storage today and a self-hosted NAS tomorrow.

## Vision

Build a clean, reusable **personal cinema interface** instead of depending on the limited playback experience of a cloud-storage app.

The storage layer should be replaceable:

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
- Use an existing high-quality player such as Infuse when it provides a better playback experience.
- Build a custom interface only where it adds real value.
- Design the system so migration to the future NAS does not require rebuilding the product.

## POC goals

1. Select the best cloud-storage backend for the project.
2. Connect a small test movie library.
3. Confirm reliable direct/streamed playback.
4. Validate subtitles, metadata, resume position and common formats.
5. Establish the architecture for the future NAS.
6. Build the first version of the personal cinema UI.

## Architecture principles

- **Storage-agnostic:** cloud today, NAS tomorrow.
- **Playback-first:** prioritize reliable playback over unnecessary custom features.
- **Self-hostable:** the final system should be comfortable running locally.
- **Portable:** avoid locking the application to a single storage provider.
- **Incremental:** every POC step should remain useful for the final system.

## Project status

**Phase 0 — Architecture & provider selection**

Next: compare cloud providers and validate the first end-to-end playback path.
