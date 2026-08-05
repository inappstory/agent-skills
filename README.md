# ias-agent-skills

Agent skills for integrating and using the [InAppStory](https://inappstory.com)
(IAS) SDK. One skill per platform — each routes to the official docs and adds a
curated layer of playbooks, pitfalls and decision guides that a single doc page
doesn't give you.

## Skills

| Skill | Platform | Package / entry point |
|---|---|---|
| `inappstory-android` | Android (Kotlin/Java, Compose) | `com.github.inappstory:android-sdk` |
| `inappstory-ios` | iOS (UIKit & SwiftUI) | `InAppStory` / `InAppStory_SwiftUI` |
| `inappstory-flutter` | Flutter | `inappstory_plugin` |
| `inappstory-react-native` | React Native | `@inappstory/react-native-sdk` |
| `inappstory-react` | React (web) | `@inappstory/react-sdk` |
| `inappstory-js` | Vanilla JS (web) | `@inappstory/js-sdk` |

## How each skill works

- **Router.** `SKILL.md` indexes every documentation topic to its live
  `docs.inappstory.com` URL. The agent fetches the exact page on demand, so page
  **content is always current** — nothing is vendored or cached to go stale.
- **Judgment layer.** `playbooks.md`, `pitfalls.md` and `decisions.md` add what a
  single page can't: end-to-end task recipes across pages, version traps and
  gotchas, and "which option to pick" decision guides. Before writing code the
  skill checks the app's SDK version and matches the existing codebase.

## Install

Replace `<owner>` with the GitHub org/user once this repo is published there.

### Claude Code (plugin)

```
/plugin marketplace add <owner>/ias-agent-skills
/plugin install inappstory@ias-agent-skills
```

Installs all six skills, namespaced `inappstory:inappstory-<platform>`.

### Any Agent Skills host (Skills CLI)

Installs into `~/.claude/skills`, `~/.codex/skills`, `~/.cursor/skills`, …

```
npx skills add <owner>/ias-agent-skills            # pick skills interactively
npx skills add <owner>/ias-agent-skills --skill '*'  # all six
```

### Antigravity

Copy the skill folders into a skills root Antigravity reads:

```bash
# Global (all projects, UI):
mkdir -p ~/.agents/skills && cp -R skills/inappstory-* ~/.agents/skills/
# Per project:
cp -R skills/inappstory-* <project>/.agents/skills/
```

### Manual (Claude Code / Codex / Cursor, works from a clone)

```bash
git clone <repo-url> ias-agent-skills
ln -s "$(pwd)/ias-agent-skills/skills/inappstory-android" ~/.claude/skills/inappstory-android
# …repeat per platform / per agent skills root
```

## Usage

Ask the relevant agent a platform question — the skill triggers on its
description:

> "How do I set up onboardings in InAppStory on iOS?"
> "Why does `new StoryManager(...)` throw in the js-sdk?"

The skill loads its judgment layer, checks your SDK version, fetches the exact
doc page, and answers against the live API.

## Source of truth

Skills are grounded in the IAS SDK docs
([repo](https://git.kiozk.ru/story/docs.git), site
<https://docs.inappstory.com>). The judgment layer is derivative synthesis with
version gates — not verbatim doc copies.

## Maintaining (on a docs release)

`scripts/sync-docs` detects when the docs drift from the skills:

```bash
scripts/sync-docs --pull    # pull docs, then report new/removed/changed pages
scripts/sync-docs --save    # accept the current docs as the baseline
```

It flags new topics missing from an index, dead links, and pages whose content
changed (a cue to refresh that topic's judgment layer). See `AGENTS.md` for the
full workflow.
