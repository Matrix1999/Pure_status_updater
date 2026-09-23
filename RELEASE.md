# Publishing a Pure Status HD update

The updater uses two GitHub surfaces:

- The `main` branch serves `pure-status.json` through raw GitHub content.
- The latest GitHub release serves the APK at a stable download URL.

## Manifest contract

`pure-status.json` must be valid UTF-8 JSON with these fields:

| Field | Type | Description |
| --- | --- | --- |
| `version_code` | integer | Android `versionCode`; update checks compare this number. |
| `version_name` | string | Human-readable version shown in the updater. |
| `apk_url` | string | HTTPS URL for the APK download. |
| `changelog` | string | Short release notes shown to the user. |
| `update_size` | string | Display value such as `24.6 MB`. |
| `force_update` | boolean | Hides the Later action when `true`. |

The Android app only presents an update when `version_code` is greater than
the installed version and `apk_url` is non-empty.

## Release sequence

Run these checks before publishing:

```bash
python3 -m json.tool pure-status.json
test "$(python3 -c 'import json; print(json.load(open("pure-status.json"))["apk_url"])')" \
  = "https://github.com/Matrix1999/Pure_status_updater/releases/latest/download/pure-status-hd.apk"
```

1. Build and sign the Android release APK.
2. Inspect the package ID and version code:

   ```bash
   aapt dump badging app-release.apk | grep -E "package:|version"
   ```

   The package must be `com.purestatus.hd`.
3. Create a GitHub release in `Matrix1999/Pure_status_updater`.
4. Upload the file as `pure-status-hd.apk` without renaming it.
5. Verify the release asset responds with an APK content type.
6. Update `pure-status.json` and push it to `main`.
7. Open the raw manifest URL and validate the JSON after GitHub finishes
   serving the new commit.

The APK must be available before the manifest is pushed. Otherwise users can
see an update prompt whose download cannot complete.

## Rollback

If a release is bad, first publish a corrected APK with a higher
`version_code`. Do not reduce the manifest version code: installed clients
will ignore a lower number by design.