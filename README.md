# au_mods

Remote mod catalog for CrewLauncher's **Mod Browser** page. The launcher reads
[`catalog.json`](catalog.json) from this repository's `master` branch:

```
https://raw.githubusercontent.com/isam-ahmed0/au_mods/master/catalog.json
```

## Contents

- `catalog.json` — the manifest (id, name, version, description, download URL,
  SHA-256, dependencies, categories).
- `mods/` — one `.zip` per mod version. Each zip contains the plugin DLL(s);
  a `BepInEx/plugins/` prefix is allowed and is flattened at install time.

> **The checked-in entries are examples.** They are harmless no-op class
> libraries with no BepInEx plugin attribute, so installing them does nothing
> in game. They exist to demonstrate browsing, filtering, dependency metadata
> and the full install flow. Replace them with real plugins, give each version
> a distinct file name, recompute `sha256`, and update `catalog.json` before
> announcing the catalog to users.

## Adding a real mod

1. Zip the plugin `.dll` files into `mods/<id>-<version>.zip`.
2. Compute the hash: `sha256sum mods/<id>-<version>.zip`.
3. Add or update the entry in `catalog.json`. Keep `id` stable across versions;
   bump `version`, change `download_url`, and update `sha256`/`size`.
4. Commit and push to `master`. The launcher picks up changes on its next
   refresh (or within the one-hour cache TTL).

Invalid JSON, duplicate ids, missing required fields or bad hashes make the
whole catalog fail validation and the launcher falls back to its cached copy.

See `docs/MOD_CATALOG.md` in the launcher repository for the full schema.
