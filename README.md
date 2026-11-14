# dsh-obsidian-skills

[English](README.md) | [中文](README.zh.md)

[Obsidian official Agent Skills](https://github.com/obsidianmd/obsidian-skills), repackaged as a [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) (DSH) plugin bundle. One install, **all seven** skills in every session — no manual directory copying. The skill files are byte-for-byte mirrors of upstream (`plugins/obsidian/skills/`), including every `references/` file.

## Included skills

| Skill | What it teaches the agent | Extra dependency |
|---|---|---|
| **obsidian-markdown** | Obsidian Flavored Markdown: wikilinks, embeds, callouts, frontmatter properties, tags, highlights, LaTeX, Mermaid | None |
| **obsidian-bases** | `.base` files: database-like views (table/cards/list/map/kanban), filters, formulas, summaries | None |
| **json-canvas** | `.canvas` files: nodes, edges, groups, layout rules and validation checklist | None |
| **defuddle** | Extract clean Markdown from web pages via Defuddle CLI | `npm i -g defuddle` |
| **knap** | Batch-render Markdown notes from JSON/CSV + templates | `npm i -g knap` |
| **obsidian-cli** | Drive the running Obsidian desktop app: read/create/search notes, tasks, properties, plugin & theme dev/debug | `obsidian` CLI (ships with installer) + desktop app running, CLI enabled |
| **obsidian-headless** | Run Obsidian Sync / Publish from the command line (`ob`) on servers, CI, or sandboxes | Node.js 22+ and `npm i -g obsidian-headless` |

The first three are pure knowledge packs (format references). The other five teach the agent to call the respective CLI tools — install/enable those tools separately for the skills to work end-to-end.

## Install

**From a local directory** (after cloning this repo):

- DSH Web GUI → **Plugins** → **Add plugin** → select this directory, or
- ask the agent: "install the bundle at `<path-to-this-directory>`".

**From a git URL:**

```
https://github.com/xiaojiahuo123/A-dsh-plugin-built-based-on-Obsidian-s-official-Skill..git
```

After enabling, open a **new session** and the seven skills appear in its skill catalog. Disable the bundle to remove them again.

## How it works

The bundle is configuration-only. Its `cordis.patch.yml` mounts a dedicated instance of `@deepseek-ai/dsh-skill-filesystem` with `includeDefaultRoots: false` and `bundledSkillDir` pointing at the package's own `skills/` directory (rank 600, so it never overrides your project or user skills with the same name). Skill files are watched; the original directory structure (`<name>/SKILL.md` plus `references/`) is preserved unmodified.

## Updating the skill contents

The skills mirror `obsidianmd/obsidian-skills` (`plugins/obsidian/skills/`). To refresh, copy the upstream skill directories into `skills/`, then bump `version` in `package.json`.

## License

MIT. Skill contents © Obsidian (obsidianmd), from [obsidianmd/obsidian-skills](https://github.com/obsidianmd/obsidian-skills) under the MIT license; see `LICENSE`.
