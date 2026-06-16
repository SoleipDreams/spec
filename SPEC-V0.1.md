# Everend Spec v0.1

Everend Spec v0.1 is the first human-readable contract for the Everend Forge ecosystem. It defines the concepts that WorldNotion, PathBranching, and engine plugins must share.

This version is intentionally lightweight: Markdown contracts plus examples. JSON Schema, formal error codes, and a CLI validator are later milestones.

## Vault

A vault is a local folder containing Markdown files and related assets. It is the canonical source for worldbuilding content.

A vault should remain readable in Obsidian-compatible tools and should not depend on app-private storage.

## Entity

An entity is a Markdown file representing a canon unit such as a character, location, culture, organization, event, concept, world, cycle, or universe.

Entity files use YAML frontmatter plus Markdown body content.

## Frontmatter

Minimum recommended fields:

~~~yaml
---
id: example-character
tipo: personaje
nombre: Example Character
estado: canon
---
~~~

Field meanings:

- id: stable identifier used by tools and runtime packages.
- tipo: entity kind.
- nombre: human-readable display name.
- estado: canon, proposal, draft, deprecated, or a project-defined equivalent.

## Stable ID

The stable ID is the durable reference used across apps. File names and display names can change; IDs should remain stable.

## Wikilink

Wikilinks are Obsidian-compatible references inside Markdown content.

~~~md
Example Character is related to [[Example-Location]] and [[Example-Organization]].
~~~

## Backlink

A backlink is derived from wikilinks. If file A links to file B, tools may show A as a backlink of B.

## Branch graph

A branch graph is an interactive narrative graph produced by PathBranching. It may reference vault entities by stable ID, but it does not replace the vault.

## Runtime package

A runtime package is a JSON/YAML export that engine plugins can execute without requiring authoring apps.

Runtime packages may include:

- Package metadata.
- Entry node.
- Nodes and choices.
- Variables.
- Conditions.
- Consequences.
- Events.
- Localization keys.
- Canon references.

## Validation report

A validation report is a shared concept for warnings and errors across tools.

Common findings include:

- Missing required frontmatter.
- Duplicate IDs.
- Broken wikilinks.
- Missing canon references.
- Broken graph transitions.
- Missing runtime assets.

## Later work

- Machine-readable JSON Schema.
- CLI validator.
- Formal error codes.
- Version compatibility matrix.
- Migration rules between spec versions.
