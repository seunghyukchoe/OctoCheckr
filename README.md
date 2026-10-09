# OctoCheckr

Native local macOS chart calibration utility. AppKit, Swift and Core Image; no server or account required.

## Public repository status

The public repository currently contains the MIT license and project documentation. Application source and binaries are not published yet: five chart reference items still require a verified redistribution basis. Build commands below describe the local development project and will become usable from the repository after source publication.

## Build and verify

```sh
./Scripts/build.sh
./Scripts/package-local.sh
CHECKR_TEST_OUTPUT="$PWD/Verification" swift test
/tmp/lua-5.1.5/src/lua Verification/test-plugin.lua "$PWD"
```

Build produces `dist/OctoCheckr.app`, as an arm64 + x86_64 universal app with an ad hoc local signature. The local packaging command creates a ZIP and SHA-256 checksum and verifies the extracted app signature. Minimum macOS13; system Inspector glass on newer macOS is provided by NSSplitViewController. No Developer ID or notarization claimed.

## Implemented

- SpyderCheckr24 and X-Rite/Calibrite Classic24 and Digital SG140, separate before/after November2014 datasets.
- CGATS Lab (.txt/.ti3/.cie) import with explicit D50/2° confirmation, chart dimensions and coordinate/file-order selection. Known conflicting measurement metadata and display/output measurements are rejected. Two neutral patches with a lightness span of10 are required (Lab chroma ≤8).
- Validated data-only JSON reference import, arbitrary rectangular6–576patch arrays, Lab D50/2° or encoded sRGB values.
- Open TIFF/JPEG/PNG from Finder’s Open With menu or drop a photo on the Dock icon. A single-image workspace opens the first supported photo in a multi-file request.
- Image rotation, horizontal/vertical flips, original restore, manual perspective corners, keyboard adjustment,8orientation alignment search. Edits are in memory; changing the source image file reloads it and clears these edits.
- Color-managed TIFF/JPEG/PNG measurement based on ImageIO content type (including `.jpe` and extensionless supported images), HSL approximation, regularized linear RGB matrix, model comparison and clipping diagnostics.
- Lightroom plugin2second refresh, explicit apply to selected photos with snapshots. Adobe XMP and rendered-sRGB33³Cube output.
- Experimental camera input ICC composition from an existing matching RGB input ICC. ColorSync and synthetic LittleCMS checks do not establish Capture One RAW compatibility.

## Remaining integration limits

Capture One is not installed. Its real RAW pipeline, profile discovery and refresh have not been tested. Its official custom ICC guidance requires restart; no no-restart support is claimed. Lightroom plugin syntax, payload validation and SDK API mocks are checked; an actual Lightroom session still needs plugin registration and controlled-photo verification. ΔE76 values shown are training error for the approximate model, not validated editor output or unseen-image accuracy. RAW ingestion and DNG profiles are not implemented.

## Reference provenance

Original files are in Research; transformed row-major definitions in Charts. Datacolor manufacturer reference is mirrored by Interfoto. X-Rite Lab D50 data are mirrored by BabelColor; Classic/SG row order is reconstructed by sample coordinate, never file order. These datasets are present in a local research build. Redistribution rights have not been established; public packaging is pending the audit in THIRD_PARTY.md. Physical card age, formulation and illumination affect results; prefer measured individual-card reference values when available.

## Native design

Apple skill plus official macOS HIG and WWDC25 AppKit guidance. `Sources/OctoCheckr/NativeViews.swift` defines app spacing tokens; system font/color/control metrics are not overridden by a fabricated Apple token set. Inspector uses native NSSplitViewItem inspector behavior; no legacy NSVisualEffectView sidebar. Control heights remain intrinsic. Toolbar is customizable. Light/dark rendered verification in Verification. Human visual acceptance is pending.

## Settings and first-run guide

Open Settings with Cmd-comma. Appearance follows the system unless overridden. Language supports English and Korean. File watching, Lightroom correction refresh, and the default export destination persist in standard app preferences. Chart reference files are stored under `~/Library/Application Support/OctoCheckr/Charts`; Settings can open this folder. Native menu/popup/toggle actions, English/Korean switching, relaunch persistence and onboarding replay have been checked in an isolated validation app; see `Verification/native-interactions.md`.

The first-run guide covers image preparation, chart alignment, and export. It is skippable and can be reopened from Help → Getting Started. Main menus and controls follow the selected language; core diagnostics, integration dialogs, and plug-in messages also have English/Korean translations. Bundled documentation opens in the selected language; web sources are in `docs/`.

## Version and release status

VERSION is the authoritative app version, currently 0.2.0. See CHANGELOG.md for changes. The build script creates and signs a clean staged app before replacing the generated bundle; deleted resources cannot linger from a previous build. MIT covers original source and documentation; THIRD_PARTY.md records material outside that license.

This is a local pre-release, not a completed public launch. Real editor validation, reference-data permissions, Developer ID signing/notarization, source publication remain pending. Public documentation is available at https://seunghyukchoe.github.io/OctoCheckr/ (English) and https://seunghyukchoe.github.io/OctoCheckr/ko/ (Korean). The public repository has been created at https://github.com/seunghyukchoe/OctoCheckr. Native language-switch and minimum-window interaction checks are recorded locally.

File-refresh and connection-state evidence: `Verification/native-file-refresh.md`. Export revision/source guards are implemented; individual native dialog race tests remain distinct from core tests.

Reference-data publication inventory: `python3 Scripts/audit-publication.py`. It currently exits2 for five unresolved items; see THIRD_PARTY.md. A clean inventory alone is not a completed release audit.

## Core API validation

`Export.xmp`, `Export.bridge` and `Export.cube` throw validation errors; callers must use `try`. XMP/bridge require exactly 24 finite HSL values between -100 and 100; revisions must be UUIDs. Cube requires a finite 3x3 matrix, finite output and 2 to 65 points per axis. Default app output is 33 cubed. These guards do not establish editor visual equivalence.
