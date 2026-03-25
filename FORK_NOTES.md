# Passcay Fork Notes

Upstream base verified on 2026-03-24:
- repo: `https://github.com/uzyn/passcay`
- ref: `main`
- local tag/commit compared: `v2.0.0` / `110b805`

Origin of the import in the host project:
- host repo: `iris_zig`
- commit: `ce3a26f9bf0f432cb092c85a7479a41b2719f6e3`
- date: `2026-03-14`
- message: `patched passcay, fixed webauthn, added parseintent endpoint`

## Functional differences from upstream

There is a single code difference:
- `src/util.zig`

Applied patch:
- `parseClientDataJson` no longer uses `json.parseFromSlice(types.ClientDataJson, ...)`
- it performs permissive parsing through `json.Value`
- it extracts only `type`, `challenge`, and `origin`
- it ignores extra browser-provided fields, especially `crossOrigin`

Practical reason:
- compatibility with real WebAuthn payloads that include additional fields in `clientDataJSON`

## Non-functional differences

Present upstream but missing from this vendored copy:
- `.github/`
- `.gitignore`
- `LICENSE`
- `docs/`

## Notes for republishing as a standalone fork

1. Restore the upstream files that are missing here (`LICENSE`, `docs`, and optionally CI workflows).
2. Keep the patch in `src/util.zig`.
3. Regenerate the package fingerprint in `build.zig.zon`.

Reference:
- `build.zig.zon` still contains `.fingerprint = 0x6afaa0c072c64272`, which is the upstream package identity.

## Suggested fork message

`passcay v2.0.0 + permissive clientDataJSON parsing for WebAuthn payloads with extra fields (e.g. crossOrigin)`
