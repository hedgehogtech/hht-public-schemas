# Changelog

Changes to the published schemas. A change that would reject a document the previous version accepted publishes as a new `v<major>` directory and is recorded here against that new version, never against the old one.

## hhtproject

### v1

- 2026-09-16: First publication. Requires `schemaVersion`, `repository`, `projectType`, `disciplines`, `harnesses`, `design`, and `gitWorkflow`. `tracker` is required when the project includes software and forbidden otherwise. Jira trackers and Confluence design stores carry their identifiers conditionally.
