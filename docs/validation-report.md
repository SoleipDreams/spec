# Validation Report

A validation report is the shared shape of compatibility feedback across Everend tools. Reports use `specVersion: "0.1"` for Everend Spec v0.1.

Minimum shape:

~~~yaml
specVersion: "0.1"
tool: worldnotion
findings:
  - code: missing_required_field
    severity: error
    file: Characters/Example.md
    field: id
    message: Entity is missing required field id.
~~~

Initial report categories:

- missing_frontmatter
- missing_required_field
- duplicate_id
- broken_wikilink
- missing_canon_ref
- broken_graph_transition
- missing_runtime_asset

Findings should include `code`, `severity`, and `message`. They may include `file`, `nodeId`, `field`, and `suggestion` when available.

Formal error code semantics are future work. For v0.1, tools should use these shared codes where possible and preserve enough location detail for a user to fix the issue.
