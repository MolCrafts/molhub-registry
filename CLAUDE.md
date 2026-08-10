---
mol_project:
  name: molhub-registry
  language: yaml
  stage: experimental
  science:
    required: false
  ci:
    config: .github/workflows/validate.yml
---

# CLAUDE.md

## What this repository is

`molhub-registry` is the data-only approval database behind MolHub. Its authored
content is limited to manifests under:

```text
artifacts/<kind>/<namespace>/<name>/<version>.yaml
```

The product implementation and language-neutral contract live in
`MolCrafts/molhub`. In particular, schema, validators, snapshot generators,
Python and TypeScript packages, the REST API, and the website do not belong in
this repository.

## Invariants

- The path is a one-to-one encoding of `kind:namespace/name@version`.
- An existing published version never changes meaning.
- Every locator pins an immutable upstream version.
- Every manifest records the DOI for the published version.
- Every artifact records a platform-published digest, a positive size, or both.
- Generated `dist/` files are disposable CI output and are never committed.
- Do not add a package manager, executable source code, copied schema, frontend,
  API, or language binding here.

Validation is owned by `MolCrafts/molhub/packages/registry-tools` and run by the
workflows in this repository.
