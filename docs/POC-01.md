# POC #1 — Shared personal cinema

## Objective

Validate the complete path from media storage to playback for multiple people:

```text
Storage (cloud first)
        ↓
Filesystem mount
        ↓
Jellyfin
        ↓
JojoFlix experience
        ↓
Users / devices
```

The POC must support:

- multiple individual user accounts
- individual playback progress
- subtitles and metadata
- direct play when possible
- transcoding when required
- local-network playback
- remote playback over HTTPS
- migration from cloud storage to a future NAS without changing the application layer
- availability without the Mac mini being powered on in the final hosted architecture

## Phase 1 — Local playback baseline

**Status: validated on Mac mini M4.**

The local server runs on a Mac mini M4 connected by Ethernet. A second device can access Jellyfin over the local network.

Validated test set:

- `Troie (2004)` — 4K HEVC Main 10, HDR10, AC3 — browser playback required transcoding to H.264/AAC.
- `Projet Dernière Chance (2026)` — 4K HEVC Main 10, AAC — Direct Streaming.
- `Gladiator (2000)` — 4K HEVC Main 10, HDR10, AAC — Direct Streaming.

Acceptance results:

- [x] library scans correctly
- [x] metadata and artwork are retrieved
- [x] playback starts reliably
- [x] audio/subtitle tracks are available
- [x] resume position works
- [x] a second user has independent progress
- [x] a second device can access the server over the local network
- [x] two simultaneous 4K streams were tested successfully
- [x] Direct Streaming works for compatible files
- [x] Transcoding works when required

Important observation: MKV itself is not the reason for transcoding. The tested HEVC/AAC MKV files streamed directly, while `Troie` required transcoding because of source/player compatibility. The future VPS therefore needs to be sized around the expected transcoding workload, not simply the number of users.

## Phase 2 — Cloud storage

Evaluate providers based on:

- cost per TB
- rclone support
- WebDAV/S3 compatibility
- streaming performance
- API/rate limits
- egress costs
- reliability
- ease of migration to a NAS

The storage provider must remain an interchangeable layer.

Target architecture:

```text
Cloud storage
      ↓
rclone / filesystem layer
      ↓
Jellyfin on hosted server
      ↓
JojoFlix / player
      ↓
Users & devices
```

## Phase 3 — Remote access

The final service must be accessible when the Mac mini is powered off. The intended production architecture is a hosted server/VPS with HTTPS and a reverse proxy.

```text
Internet
   ↓
HTTPS / domain
   ↓
Reverse proxy
   ↓
Jellyfin / JojoFlix
   ↓
Cloud media storage
```

Do not expose Jellyfin directly to the public internet as the final architecture.

## Phase 4 — Multi-user test

Validated locally with:

- owner/admin account
- coloc test account

Next test later:

- owner/admin account
- coloc account
- friend account
- simultaneous remote sessions

Validate that each user has independent authentication and playback state.

## Phase 5 — JojoFlix UI

Only after the playback infrastructure is reliable, start the custom interface.

The UI should consume a stable media/playback layer rather than owning storage logic.

The product name is **JojoFlix**; `Media Home` remains the technical/development project name.

## Definition of Done

- [x] Test library visible
- [x] Metadata working
- [x] Audio/subtitles tested
- [x] Resume working per user
- [x] At least two users can stream independently
- [x] Local-network playback working
- [x] Direct streaming and transcoding behavior validated
- [ ] Remote HTTPS access working
- [ ] Cloud storage validated
- [ ] VPS-hosted architecture validated
- [ ] Cloud → NAS migration path documented
- [ ] First JojoFlix interface can sit on top of the validated backend
