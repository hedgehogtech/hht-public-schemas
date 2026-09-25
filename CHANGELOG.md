# Changelog

Changes to the published schemas. A change that would reject a document the previous version accepted publishes as a new `v<major>` directory and is recorded here against that new version, never against the old one.

## hhtproject

### v2

- 2026-09-25: `design` is replaced by `documentation`, a required array of Confluence mirrors that may be empty. The repository copy under `docs/` is always the source, and every entry is synced: a published document goes to each one. An entry carries `kind`, `site`, `spaceKey`, and `documentationFolder`, with optional `specsFolder` and `designsFolder`; folders are numeric Confluence content IDs rather than URLs. `spaceUrl`, `designRoot`, and `repositoryFolder` are removed, and the `markdown` store is expressed as an empty array. `schemaVersion` is `2`. `tracker` is unchanged apart from its `local` description, which now names `docs/tasks/`.

### v1

- 2026-09-16: First publication. Requires `schemaVersion`, `repository`, `projectType`, `disciplines`, `harnesses`, `design`, and `gitWorkflow`. `tracker` is required when the project includes software and forbidden otherwise. Jira trackers and Confluence design stores carry their identifiers conditionally.
