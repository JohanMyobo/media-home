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
Media Home experience
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

## Phase 1 — Local playback baseline

Before introducing cloud storage, validate Jellyfin with a small local test library.

Test set:

- 1 x 1080p H.264 movie
- 1 x HEVC/H.265 movie if available
- 1 x subtitle file (SRT)
- 1 x episode of a series

Acceptance criteria:

- library scans correctly
- metadata is retrieved
- playback starts reliably
- subtitles work
- resume position works
- a second user has independent progress

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

## Phase 3 — Remote access

Expose the service securely through HTTPS and a reverse proxy.

Target architecture:

```text
Internet
   ↓
HTTPS / domain
   ↓
Reverse proxy
   ↓
Jellyfin
   ↓
Media storage
```

Do not expose Jellyfin directly to the public internet as the final architecture.

## Phase 4 — Multi-user test

Test simultaneously with:

- owner/admin account
- coloc account
- friend account

Validate that each user has independent authentication and playback state.

## Phase 5 — Media Home UI

Only after the playback infrastructure is reliable, start the custom interface.

The UI should consume a stable media/playback layer rather than owning storage logic.

## Definition of Done

- [ ] Test library visible
- [ ] Metadata working
- [ ] Subtitles working
- [ ] Resume working per user
- [ ] At least two users can stream independently
- [ ] Remote HTTPS access working
- [ ] Cloud storage validated
- [ ] Cloud → NAS migration path documented
- [ ] First Media Home interface can sit on top of the validated backend
