# HHT public schemas

Published JSON Schemas for the machine-readable files Hedgehog Technologies produces. They are here so anyone can validate an HHT artifact without access to the repository that produced it: a client checking a delivered file, a CI job gating a contribution, or an editor offering completion while someone writes one by hand.

This repository holds the schemas only. It holds no HHT project data, and nothing here is a template to copy into a new project.

## Schemas

| Schema | Current version | Describes |
| --- | --- | --- |
| HHT project manifest | v2 | `hhtproject.json`, the per-repository configuration naming a repository's identity, work tracker, documentation mirrors, and Git workflow. |

Every schema is written against [JSON Schema draft 2020-12](https://json-schema.org/draft/2020-12/schema).

## Layout

```
json/
└── <schema-name>/
    └── v<major>/
        └── <schema-name>.schema.json
```

Each schema versions independently, so the schema name comes before the version. A published version directory is frozen: its URL keeps serving that schema for as long as this repository exists.

## Using a schema

Reference a schema by its URL, which is also its `$id`:

```
https://raw.githubusercontent.com/hedgehogtech/hht-public-schemas/main/json/hhtproject/v2/hhtproject.schema.json
```

Point an editor at it from inside the document being validated:

```json
{
  "$schema": "https://raw.githubusercontent.com/hedgehogtech/hht-public-schemas/main/json/hhtproject/v2/hhtproject.schema.json",
  "schemaVersion": 2,
  "repository": "hedgehogtech/example-repo"
}
```

Validate from the command line with [check-jsonschema](https://github.com/python-jsonschema/check-jsonschema):

```bash
check-jsonschema --schemafile https://raw.githubusercontent.com/hedgehogtech/hht-public-schemas/main/json/hhtproject/v2/hhtproject.schema.json hhtproject.json
```

Or with [ajv-cli](https://github.com/ajv-validator/ajv-cli), against a local copy:

```bash
ajv validate --spec=draft2020 -s json/hhtproject/v1/hhtproject.schema.json -d hhtproject.json
```

`raw.githubusercontent.com` serves these files as `text/plain` and rate limits unauthenticated clients. A validator that fetches the URL on every run will eventually be throttled, so cache the file or vendor a copy in any build that runs often.

Substituting a commit SHA for `main` in the URL pins the exact bytes. A frozen version directory makes this unnecessary for correctness, but it removes the branch from the path.

## Versioning

The major version is in the URL. A schema change that would reject a document the previous version accepted publishes as a new `v<major>` directory alongside the old one, which keeps working unchanged. Additive changes that leave every existing document valid are made in place, and `CHANGELOG.md` records them.

`hhtproject.json` also carries `schemaVersion` as a field, currently `2`, mirroring the directory it validates against. A reader checks that field before anything else, so a manifest written against a newer format is reported as a version mismatch rather than as a list of unknown keys.

## Licence

Licensed under [CC BY-ND 4.0](https://creativecommons.org/licenses/by-nd/4.0/). See `LICENSE`.

Copy these schemas, redistribute them, and use them to validate anything, commercially or otherwise, with attribution to Hedgehog Technologies. Do not publish a modified version: a divergent schema carrying HHT's identity would validate documents HHT does not recognize. If a schema needs to change to cover your case, open an issue.

## Contributing

Each schema here is a published copy of one maintained inside HHT's own tooling, so a pull request editing a schema file lands in the wrong place and cannot be merged as written. Open an issue instead, describing the document that failed to validate and what it should have accepted.
