# PiggieTV Plugin Catalog Rules

This repository is a generated distribution mirror of the companion plugin embedded in `../Jellyfin-Web-PiggieTV/src/ptv/plugin/Jellyfin.Plugin.PiggieTV`. It does not own an independent product version.

## Version authority

- `PtvPluginVersion` in the embedded plugin project is the canonical version authority.
- Never bump the catalog manifest or package name independently. First bump and verify the embedded plugin, then regenerate this catalog from its exact published payload.
- Each material user request that changes plugin source bumps the canonical PiggieTV version exactly once for the complete request. Internal Codex tool calls, agent messages, retries, builds, tests, packaging, and deployment steps do not cause additional bumps.
- Use product versions `major.minor.patch`, with every component limited to `0..99`. Routine requests increment `patch` by one. Carry `0.0.99` to `0.1.0`. Do not carry `0.99.99` into `1.0.0`; a major-version change requires an explicit major-release decision.
- Jellyfin/.NET represents the product version with a fourth zero component. For example, product release `0.5.0` is published as `0.5.0.0`.
- Jellyfin compatibility is independent of the PiggieTV release number. Do not change `targetAbi` or the Jellyfin package target merely to match the product version.

## Catalog regeneration

1. Test and publish the embedded plugin to `../Jellyfin-Web-PiggieTV/src/ptv/plugin/bin`.
2. Confirm the payload contains exactly the matching DLL, deps JSON, PDB, XML documentation, and `meta.json`.
3. Package those five files at the ZIP root using the canonical four-part version in the filename.
4. Mirror the embedded plugin GUID, version, changelog, `targetAbi`, and timestamp into `manifest.json`.
5. Recalculate the ZIP MD5 for Jellyfin's manifest `checksum`, then validate the archive contents and assembly/manifest version agreement.
