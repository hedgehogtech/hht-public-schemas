# Changelog

Changes to the published schemas. A change that would reject a document the previous version accepted publishes as a new `v<major>` directory and is recorded here against that new version, never against the old one.

## hhtproject

### v2

- 2026-10-20: The `gitWorkflow` and `gitWorkflow.preset` descriptions now say a repository whose manifest is missing or unusable runs as `solo`, that `solo` commits and pushes each verified change on its own, and that the only force-push permitted is `--force-with-lease` with `--force-if-includes` to a feature branch. Description text only: v2 accepts and rejects exactly the documents it did before.
- 2026-09-25: `design` is replaced by `documentation`, an array holding exactly one `local` entry, the repository tree the workflow writes and reads, and any number of `confluence` entries, each a synced mirror of it. Every folder is a subfolder of the entry's `rootFolder`: `specsSubfolder`, `plansSubfolder`, `designsSubfolder`, and `decisionsSubfolder` on either kind, and `researchSubfolder`, `ideasSubfolder`, and `outOfScopeSubfolder` on the local entry only, since those notes are not published. All are optional, and the defaults make `{ "kind": "local" }` the `docs/` tree: `docs/specs/`, `docs/plans/`, `docs/designs/`, `docs/decisions/`, `docs/research/`, `docs/ideas/`, and `docs/out-of-scope/`. A local folder is a repository-relative path; a Confluence entry requires `site`, `spaceKey`, and a `rootFolder` content ID, and names its subfolders by title. `spaceUrl`, `designRoot`, and `repositoryFolder` are removed. A local `tracker` gains an optional `tasksSubfolder` under the same root, `tasks/` by default. `schemaVersion` is `2`.

### v1

- 2026-09-16: First publication. Requires `schemaVersion`, `repository`, `projectType`, `disciplines`, `harnesses`, `design`, and `gitWorkflow`. `tracker` is required when the project includes software and forbidden otherwise. Jira trackers and Confluence design stores carry their identifiers conditionally.
