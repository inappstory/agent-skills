# ias-agent-skills

Agent skills for working with the [InAppStory](https://inappstory.com) (IAS) SDK.

The skills teach an AI agent how to integrate and use IAS across its supported
platforms — Android, iOS, React Native, JavaScript, React and Flutter — grounded
in the official IAS SDK documentation.

## Source of truth

Skills are built from the IAS SDK docs:

- **SDK guides** — per-platform integration (`sdk-guides/`)
- **Glossarium** — console concepts: targeting, personalization, statistics, appearance
- **UGC guides** — user-generated content
- **API / webhooks / on-premise / security** — reference material

Docs repo: <https://git.kiozk.ru/story/docs.git>

## Structure

```
skills/
  <skill-name>/
    SKILL.md      # skill definition + instructions
    ...           # supporting files
```

Each skill is a self-contained directory following the standard agent-skill
format (`SKILL.md` with frontmatter + instructions).

## Creating a skill

Skills here are authored with the `skill-creator` skill, which scaffolds the
directory, writes `SKILL.md`, and helps refine the description for reliable
triggering. See its docs for the workflow.
