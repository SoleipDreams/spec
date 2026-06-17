# Runtime Package

A runtime package is a JSON/YAML export produced by authoring tools such as PathBranching and consumed by engine plugins.

Runtime packages should include:

- specVersion
- packageId
- entryNodeId
- canonRefs
- variables
- localization
- nodes

`specVersion` must be the string `"0.1"` for Everend Spec v0.1 runtime packages.

`canonRefs` reference vault entities by stable ID. When a runtime package includes `canonRefs[].kind`, it should match the referenced entity `type` when that information is available.

Runtime packages must not require WorldNotion or PathBranching to be installed at runtime.

See [../examples/runtime-package.json](../examples/runtime-package.json) and [../examples/runtime-package.yaml](../examples/runtime-package.yaml).
