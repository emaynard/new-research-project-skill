# new-research-project

A Claude skill that scaffolds a new genealogical research project inside
an Obsidian vault using the [Charted Roots](https://github.com/banisterious/obsidian-charted-roots)
plugin. Creates a Research Project index note plus a seeded Individual
Research Note, both flat in the vault's shared `Research/` folder, using
Charted Roots' `cr_type` frontmatter so the project shows up in existing
Bases views immediately.

Adapted from the design of the
[`gra` skill](https://github.com/DigitalArchivst/Open-Genealogy/tree/main/skills/gra)
in Steve Little's [Open-Genealogy](https://github.com/DigitalArchivst/Open-Genealogy)
(Genealogy AI Starter Workspace), reworked to avoid duplicating files that
Charted Roots already handles vault-wide (sources, GPS methodology
instructions, templates). All credit for the original project structure
and GPS-aligned research workflow goes to Steve Little/DigitalArchivst -
this skill only adapts it for Charted Roots vaults.

## Requirements

- An Obsidian vault using the Charted Roots plugin
- `Templates/GRA/` templates installed in that vault (Research Project,
  Research Log Entry, Research Journal, Individual Research Note,
  Research Report) - see that folder's README.md for the full design
- The `gra` and/or `family-history-planning` skills for GPS methodology

## Installation

Download `new-research-project.skill` from the
[Releases](../../releases) page (or build it yourself with
`package_skill.py` from the skill-creator toolkit) and install it via
Settings > Capabilities in Claude/Cowork.

## License

CC-BY-NC-SA-4.0 - see LICENSE.
