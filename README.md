# Pure Status HD updater

This repository is the public update channel for **Pure Status HD**. The
Android app checks `pure-status.json` on the splash screen and opens its
bundled updater when `version_code` is newer than the installed build.

## Files

- `pure-status.json` — the update manifest consumed by the Android app.
- `index.html` — the current Munowatch-derived Pure Status updater preview for
  the public update channel.
- `RELEASE.md` — the release procedure and manifest contract.

The Android app keeps its runtime updater page in
`app/src/main/assets/pure_status_update.html`; it does not download HTML from
this repository. The repository's `index.html` is the single web preview, so
there is no duplicate updater HTML file in the update channel.

## Important release asset

The manifest points to this stable URL:

```text
https://github.com/Matrix1999/Pure_status_updater/releases/latest/download/pure-status-hd.apk
```

Every published release must include an APK asset with the exact filename
`pure-status-hd.apk`. GitHub's `latest` release redirect keeps the URL stable
when a newer release is published.

## Quick release checklist

1. Build a signed release APK for `com.purestatus.hd`.
2. Confirm its `versionCode` is greater than the previous manifest value.
3. Create a GitHub release in this repository.
4. Upload the APK as `pure-status-hd.apk`.
5. Update `pure-status.json` with the new version, changelog, size, and release
   date.
6. Commit and push the manifest. The app will see the update on its next
   splash check.

Do not publish a manifest that refers to an APK which has not already been
uploaded. The app validates the remote version and URL but does not verify a
release asset before showing the update dialog.
