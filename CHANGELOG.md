# Versions

## 0.2.0 — local pre-release

- Keep last-valid Lightroom status during partial rewrites without extending its original expiry; missing files clear status immediately.

- Run one automatic orientation search at a time; restore action availability after success, failure or a superseded result.

- Verify both Mach-O slices match the advertised minimum macOS version before packaging and after ZIP extraction.

- Validate all24 HSL values and Lightroom revision identifiers before XMP/bridge serialization. Library XMP/bridge export now throws validation errors.

- Reject invalid LUT dimensions, malformed matrices and nonfinite output before saving; verify identity cube RGB ordering. Library cube export now throws validation errors.

- Keep export actions disabled throughout background ICC composition, including intervening analysis/button refreshes.

- Align native inspector actions and helper text to shared form columns; name export buttons and describe the actual HSL/RGB model for each destination in English/Korean.

- Invalidate correction immediately when a watched source changes or disappears. Detect atomic replacements by file identity, require stable observations, compare metadata across decode, and retain watching after failed reads.
- Recheck watched-source freshness and correction revision around export dialogs and before ICC writes; suppress stale Lightroom sends.
- Bound Lightroom status reads and reject stale/future/malformed heartbeats; clear connection state when the status file disappears.

- Restructure the native inspector around shared-width controls; remove duplicate alignment actions and hide empty patch comparison. Add a native empty-state Open Photo button.
- Name settings and main input controls for accessibility, refresh custom labels on language changes, and verify settings persistence and onboarding through actual native interactions.
- Detect supported image formats from ImageIO contents rather than filename suffix; accept `.jpe`/extensionless supported images and reject renamed unsupported formats without a redundant full-image decode.

- Original multi-resolution app icon and Finder/Dock photograph opening (TIFF/JPEG/PNG); app registers as an alternate viewer.
- Native inspector layout with shared form columns and native toolbar actions.
- Persistent settings for appearance, language, file watching, Lightroom refresh, and default export destination.
- Three-step, skippable first-run guide with Help-menu replay.
- English and Korean settings, onboarding, main controls, and status messages. Core diagnostics, integration dialogs, Lightroom SDK messages and bundled documentation are also localized.
- Background orientation analysis, preview work only when enabled, and fewer bridge writes during corner dragging.
- Reset clears mirrored chart orientation.
- CGATS Lab reference import with native layout/measurement confirmation, decimal-comma support, A1 coordinate ordering and strict table validation.
- Chart reimports replace a canonical atomic snapshot and survive relaunch; invalid replacement preserves the saved reference. Reference reads are bounded to one megabyte.

- Universal arm64/x86_64 app build and local ZIP with SHA-256 checksum; extracted signature verified.
- Plugin updates preserve a backup and reject unsafe destinations.
- Stricter UUID validation in the Lightroom bridge.
- Image actions and preview disable while no image is available or loading; failed loads clear the restoration source.
- Reopening the first-run guide starts at the beginning after completion or closing.
- Bilingual responsive documentation, verified in desktop and narrow mobile browser renders.

This is a locally validated development iteration. Public distribution, complete localization, real-editor integration verification, reference-data redistribution clearance, Developer ID signing and notarization are still pending. It is not a launch-ready release.

## 0.1.0 — initial local prototype

- SpyderCheckr24 and rectangular JSON chart references.
- Color-managed TIFF/JPEG/PNG sampling and perspective alignment.
- HSL approximation, linear RGB matrix, XMP, sRGB cube LUT, and experimental camera input ICC export.
- Lightroom Classic bridge plug-in with explicit photo application and snapshots.
- Rotation, horizontal/vertical flips, original-photo restore, and patch comparison.

Compatibility evidence and limitations belong in README.md and THIRD_PARTY.md; version numbers alone do not establish integration support.

### ICC input hardening

- Verify actual TIFF source format, 16-bit sample depth and ICC tag before experimental camera export; preserve metadata through image edits.
- Read the selected RGB input ICC once with a 16 MiB bound and reuse that immutable snapshot during export.
- Add tests for disguised JPEGs, 8-bit TIFFs, metadata preservation and oversized/malformed base files.

- Finish an already-detected source reload when file watching is disabled, avoiding a permanently disabled workspace.

- Lightroom plug-in build2 reports applied only when synchronous catalog write access returns executed; handle timeout/aborted results with a localized warning.

- Group bilingual guide conditions by task, give chart references their own navigation entry, and add semantic table headers and visible keyboard focus. Verify latest content on light/dark desktop and narrow viewports.

- Reject JSON references with single or duplicate neutral indices, or white/black indices missing from the neutral list; retain valid Classic/SG and custom reference imports.
