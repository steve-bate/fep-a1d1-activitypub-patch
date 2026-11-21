# FEP-a1d1: ActivityPub Patch

**Status:** DRAFT · **Type:** implementation · **Author:** Steve Bate

## Overview

ActivityPub's Client-to-Server Partial Update relies on shallow top-level replacement and uses
JSON `null` to signal property removal. In compacted JSON-LD, `null` values are elided, so a
deletion signalled this way can be lost in transit. The partial-update representation also
overloads `id` to identify the *target* object rather than the update itself, and it cannot
touch nested properties.

This FEP introduces a `Patch` activity based on [JSON Patch (RFC 6902)](https://datatracker.ietf.org/doc/html/rfc6902):

- The patch operations live in a separate `PatchOperations` object, leaving the `target`
  object untouched.
- Operations (`add`, `remove`, `replace`, `move`, `copy`, `test`) address the target using
  [JSON Pointer (RFC 6901)](https://www.rfc-editor.org/rfc/rfc6901), so nested properties can
  be updated.
- The FEP defines the JSON-LD context for `Patch` and `PatchOperations`.

When a `Patch` is posted to an outbox, the server applies the authorized operations and should
then send an `Update` notification containing the full updated object.

## Files

- [`fep-a1d1.md`](fep-a1d1.md) — the proposal
- [`fep-a1d1.jsonld`](fep-a1d1.jsonld) — JSON-LD context

## The FEP

- Document: <https://github.com/steve-bate/fep-a1d1-activitypub-patch/blob/main/fep-a1d1.md>
- Repository: <https://github.com/steve-bate/fep-a1d1-activitypub-patch>
- Discussion: <https://github.com/steve-bate/fep-a1d1-activitypub-patch/issues>

## License

This work is released under [CC0 1.0 Universal](LICENSE.md) (public domain dedication).
See [LICENSE.md](LICENSE.md).
