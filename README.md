# NYC In Focus Public Releases

This repository is the public-reader release endpoint for NYC In Focus applications.

It contains only approved, reader-safe, immutable release files. It must never contain:
- raw source snapshots
- source credentials
- private location evidence
- reviewer notes
- duplicate candidates
- pipeline code
- unapproved event records

## Reader flow

1. The app fetches `current.json`.
2. It fetches the referenced immutable `release-manifest.json`.
3. It verifies every referenced file's release ID, byte size, and SHA-256 checksum.
4. If any verification fails, it retains the last verified release.

## Release layout

```text
current.json
releases/<release-id>/
  release-manifest.json
  events.json
  taxonomy.json
  temporal-projection.json
  changes.json
  checksums.json
  missed/<yyyy-mm-dd>.json
```

Only the protected promotion workflow may add a release or update `current.json`. Each versioned release is immutable. Rollback changes only `current.json` to a prior verified manifest.
