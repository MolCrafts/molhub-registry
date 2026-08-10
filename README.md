# molhub-registry

The approved manifest database for [MolHub](https://github.com/MolCrafts/molhub).

This repository contains data only:

```text
artifacts/<kind>/<namespace>/<name>/<version>.yaml
```

For example, `artifacts/dataset/molcrafts/qm9/v2.yaml` is the record behind
`dataset:molcrafts/qm9@v2`. Published versions are immutable: add a new file for
a new release instead of changing what an existing coordinate means.

The schema, validator, snapshot builder, Python package, TypeScript SDK, REST
API, and website all live in
[`MolCrafts/molhub`](https://github.com/MolCrafts/molhub). Generated
`dist/registry.json` and `dist/registry.yaml` are built by CI and are not
committed here.

## Submit a manifest

The normal path is the submission form in the MolHub website. It validates the
same contract as CI, stores review status, and creates a registry pull request
after approval. GitHub remains available for contributors who prefer to work
directly with YAML.

For a direct contribution:

1. Add one YAML file at the coordinate-derived path above.
2. Include the DOI for the exact published version.
3. Pin every locator to an immutable record, release, or commit.
4. Give each artifact a platform-published `digest`, a positive `size`, or both.
5. Open a pull request.

To run the same checks locally, keep `molhub` and `molhub-registry` beside each
other:

```bash
git clone https://github.com/MolCrafts/molhub.git
git clone https://github.com/MolCrafts/molhub-registry.git
cd molhub
npm ci
npm run registry:validate -- ../molhub-registry/artifacts
npm run registry:build -- ../molhub-registry/artifacts ../molhub-registry/dist
```

The manifest contract is documented in
[`spec/manifest.schema.yaml`](https://github.com/MolCrafts/molhub/blob/main/spec/manifest.schema.yaml).

## Repository contract

- `artifacts/` is the only authored database content.
- No application or language-binding code belongs here.
- No copy of the schema belongs here.
- `dist/` is disposable output and must not be committed.
- CI checks out the MolHub toolchain and validates this database with it.

## License

BSD-3-Clause.
