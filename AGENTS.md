# AGENTS.md

Vendor-agnostic context for any AI coding agent working on **ias-agent-skills**.
This is the single source of truth; `CLAUDE.md` is a one-line `@AGENTS.md` shim
so Claude Code reads it too.

## What this repo is

A standard, installable **agent-skills repository**: skills that teach an AI
agent how to integrate and use the [InAppStory](https://inappstory.com) (IAS)
SDK across Android, iOS, React Native, JavaScript, React and Flutter. See
`README.md` for what it is and how to install it.

## Layout

```
skills/inappstory-<platform>/   # the product — one skill per platform
  SKILL.md                      #   router (topic→docs URL index) + workflow
  playbooks.md pitfalls.md decisions.md   # curated judgment layer
.claude-plugin/                 # Claude Code plugin + marketplace manifests
scripts/sync-docs               # maintainer tool: detect docs drift
tools/book-to-skill/            # vendored authoring tool (not shipped)
AGENTS.md  CLAUDE.md  README.md
```

## Working rules

- Skills follow the standard agent-skill format: a `SKILL.md` with frontmatter
  (`name`, `description`) plus supporting files, one directory per skill. Author
  new ones with the `skill-creator` skill.
- Each `inappstory-*` skill is a **router + judgment layer**: `SKILL.md` indexes
  every doc topic to its live `docs.inappstory.com` URL and the agent fetches on
  demand; `playbooks/pitfalls/decisions.md` add cross-page recipes, version traps
  and decision guides the docs don't give in one page.
- Skills are grounded in the IAS SDK docs (<https://git.kiozk.ru/story/docs.git>,
  public site <https://docs.inappstory.com>). Don't invent SDK behavior — the
  judgment layer is derivative synthesis with version gates, never verbatim copies.

## Updating skills on a docs release

Page **content** is fetched live, so it never goes stale. Two things can drift,
and `scripts/sync-docs` detects both against a saved baseline
(`scripts/sync-docs.state`):

```bash
scripts/sync-docs          # report drift (exit 1 if any)
scripts/sync-docs --pull   # git pull the docs repo first, then report
scripts/sync-docs --save   # accept the current docs as the new baseline
IAS_DOCS=/path/to/in-app-stories-docs/docs scripts/sync-docs
```

It reports, per platform: `+` new topic pages missing from a skill's index,
`-` dead links to removed/renamed pages, and `~` pages whose content changed
(a signal that topic's judgment layer may need a refresh). It is read-only — it
never rewrites the curated index or judgment files; refreshing those is an LLM
pass (re-read the changed page, re-distill). Workflow on a docs release:
`--pull` → read the report → fix the flagged index/judgment → `--save`.
