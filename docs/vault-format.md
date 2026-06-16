# Vault Format

An Everend vault is a local folder of Markdown files and assets. The vault is the canonical source for worldbuilding content.

## Entity files

Entity files use YAML frontmatter and Markdown body content.

Minimum recommended frontmatter:

~~~yaml
---
id: example-character
tipo: character
name: Example Character
status: draft
---
~~~

## Stable IDs

The id field is the durable cross-tool reference. Names, aliases, and file paths may change; IDs should remain stable.

## Wikilinks

Wikilinks use Obsidian-compatible syntax:

~~~md
[[Example-Character]]
[[Example-Location|example location]]
~~~

Tools may resolve wikilinks by file basename, aliases, or future index metadata.

## App storage

Apps may create caches, but caches must be rebuildable from vault files. The source of truth remains the Markdown vault.
