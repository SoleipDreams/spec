# Vault Format

An Everend vault is a local folder of Markdown files, assets, and optional Everend metadata. The vault is the canonical source for worldbuilding and narrative planning content.

Vaults should stay readable in Obsidian-compatible tools. Everend tools may add caches, but caches must be rebuildable from Markdown files and optional `.everend` metadata.

## Entity files

Entity files use YAML frontmatter and Markdown body content.

Minimum recommended frontmatter:

~~~yaml
---
id: example-character
type: character
name: Example Character
status: draft
tags: [example]
aliases: [Example Alias]
---
~~~

Required fields:

- id: stable identifier used across tools and runtime packages.
- type: open string describing the entity kind.
- name: human-readable display name.
- status: canon, proposal, draft, deprecated, or a project-defined equivalent.

Common optional fields:

- tags: list of labels for search and grouping.
- aliases: alternate display names or wikilink candidates.
- parentId: stable ID of a parent entity.
- childrenIds: list of child entity stable IDs.

Unknown frontmatter fields are allowed and should be preserved by editing tools.

## Taxonomy

Everend Spec v0.1 recommends these starter types:

- character
- location
- organization
- event
- concept
- item
- world
- cycle
- universe
- story
- arc
- scene
- quest

Projects may define their own types. The `type` field is not a closed enum.

## Folder Descriptions

Folders may have associated description files to document their contents and purpose. These files follow a simple naming convention:

- **Folder descriptions**: A file named `{FolderName}.md` at the same level as the folder it describes
  - Example: `Characters/` folder → `Characters.md` file
  - These files are excluded from entity validation
  - Recommended frontmatter: `type: "folder-description"`, `folder: "{FolderName}"`

- **Vault descriptions**: A file named `{VaultName}.md` at the vault root
  - Describes the overall world/universe
  - Recommended frontmatter: `type: "world-description"`

Folder and vault description files are optional. Tools should treat them as documentation, not as entities for runtime packages or graph validation.

## Taxonomy manifest

A vault may include `.everend/taxonomy.yaml` to describe project-specific types and properties. The manifest is optional.

~~~yaml
specVersion: "0.1"
types:
  item:
    label: Item
    description: Portable object, relic, tool, artifact, or inventory-relevant entity.
    properties:
      rarity:
        type: select
        options: [common, rare, legendary]
      material:
        type: text
      relatedCharacters:
        type: entityRefList
~~~

Supported property types:

- text
- number
- boolean
- date
- select
- multiSelect
- entityRef
- entityRefList

## Stable IDs

The id field is the durable cross-tool reference. Names, aliases, and file paths may change; IDs should remain stable.

## Hierarchies

Hierarchies are expressed with stable IDs in frontmatter.

~~~yaml
---
id: iron-crown
type: item
name: Iron Crown
status: canon
parentId: imperial-regalia
---
~~~

Tools may use `parentId` and `childrenIds` to render trees. Wikilinks remain useful for narrative relationships, but structured hierarchy should use these frontmatter fields.

## Wikilinks

Wikilinks use Obsidian-compatible syntax:

~~~md
[[Example-Character]]
[[Example-Location|example location]]
~~~

Tools may resolve wikilinks by file basename, aliases, or future index metadata.

## App storage

Apps may create caches, but caches must be rebuildable from vault files. The source of truth remains the Markdown vault and optional portable `.everend` metadata.
