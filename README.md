# au_mods

Remote mod catalog for CrewLauncher's **Mod Browser** page. The launcher reads
[`catalog.json`](catalog.json) fresh from this repository's `master` branch:

```
https://raw.githubusercontent.com/isam-ahmed0/au_mods/master/catalog.json
```

No caching: every catalog load fetches this file again. See
`docs/MOD_CATALOG.md` in the launcher repository for the full schema.

## Contents

- `catalog.json` — the manifest (id, name, description, download URL,
  dependencies, categories). There is no `version`, `sha256` or `size` field:
  those change with every release and would mean editing the catalog constantly.
- `mods/` — example plugin ZIPs. Paths inside a zip are flattened to their
  basename at install time, and only `.dll` files are copied.

> **The checked-in entry is an example.** It points at a placeholder release
> asset and does nothing in game. Replace it with a real mod entry before
> announcing the catalog to users.

## Adding a real mod

1. Build a `.zip` containing the plugin `.dll` files, or use a single `.dll`.
2. Publish it as a GitHub release asset with a **stable filename** (e.g.
   `CoolMod.zip`) in the mod's own repository.
3. Add one entry to `catalog.json` with `id`, `name`, `description` and
   `download_url` set to
   `https://github.com/<owner>/<repo>/releases/latest/download/CoolMod.zip`.
4. Commit and push to `master`. Users see the new entry immediately and press
   **Reinstall** in the Mod Browser to pull the current asset.

For every later release, step 2 is all you need — keep the same asset name and
the catalog never changes. Invalid JSON, duplicate ids or missing required
fields make the catalog fail validation and the Mod Browser shows an error.
