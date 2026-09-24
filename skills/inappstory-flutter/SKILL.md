---
name: inappstory-flutter
description: "Integrate and use the InAppStory (IAS) SDK on Flutter — FeedStoriesWidget, single stories, onboardings, in-app messaging, games, goods, banners, favorites, appearance, events, and more. Use when adding, configuring, or debugging the InAppStory Flutter/Dart plugin, or answering how the Flutter IAS SDK works."
---

<!--
Vendor-neutral: no `allowed-tools` on purpose. Routes to the public docs and
expects the host agent to fetch a URL (Claude: WebFetch; others: a browser/fetch
tool). Agents without a fetch tool degrade gracefully — the URLs are clickable.
argument-hint: [topic, e.g. feed-stories-widget, in-app-messaging, appearance]
-->

# InAppStory SDK — Flutter

This skill routes to the **official InAppStory Flutter docs**. The docs are the
source of truth and change often, so this skill does not copy them — it points
to the exact page and expects you to **fetch it on demand**.

## How to use

1. Find the relevant topic in the index below.
2. **Fetch that page** (`WebFetch <url>`) and answer from the live content —
   never guess SDK APIs, versions, or pub.dev coordinates from memory.
3. New to the SDK? Start with **How to get started**, then **InAppStoryManager**
   and **Options**.
4. If you have no fetch tool, give the user the exact URL to open.

Base URL: `https://docs.inappstory.com/sdk-guides/flutter/`

## Judgment layer (read these first — what a doc page won't tell you)

- **[playbooks.md](playbooks.md)** — end-to-end recipes (feed, onboardings, single
  story, IAM, switch user, banners) including the mandatory native Android steps.
- **[pitfalls.md](pitfalls.md)** — grounded gotchas: native setup (`initSDK` in
  `Application`, `MainActivity : InAppStoryActivity`), async `initWith`, singleton
  `.instance` migration, HostApi→singleton renames (0.8.0).
- **[decisions.md](decisions.md)** — `MainActivity` base class by version, singleton
  vs old HostApi, which list widget, callback mixins.

## Intake — ask before you write

Two quick checks before any integration work:

1. **Underspecified request? Ask, don't guess.** If the user didn't say *where*
   the UI goes (which screen/widget) or *which* feature they mean, ask before
   writing — a feed on the wrong screen is wasted work.
2. **First integration? Get the integration key.** If the codebase grep (below)
   finds no existing IAS setup, this is a fresh integration: ask the user for their
   **integration key** (`apiKey`) — init fails without it. If a setup already
   exists, reuse its key; don't ask.
3. **Verify it? Decide now (first integration only).** Offer to build & run the app
   after wiring it up, so a first integration isn't left untried. Ask the depth —
   smoke-run (build + launch, watch the feed load), also a minimal test, or skip —
   batched with the questions above. A "yes" here is the go-ahead; don't re-ask
   before running. See **Verify a first integration** below for how.

## Before you answer or write integration code

1. **Check the plugin version** in `pubspec.yaml` (`inappstory_plugin: X.Y.Z`);
   if absent, ask. The API changed across 0.x (singletons, 0.8.0 renames) — answer
   for that version and fetch **migrations** for deltas.
2. **Verify the native Android setup** — most "doesn't work on Android" reports are
   a missing `InAppStoryPlugin.initSDK` or `MainActivity` not extending
   `InAppStoryActivity`. Check these before debugging Dart.
3. **Write against the repo, not a blank slate (codebase-aware).** Grep for
   `InAppStoryPlugin(` / `InAppStoryManager.instance` / `FeedStoriesWidget` and
   `inappstory_plugin` in `pubspec.yaml`. **Found** → *extend* it: reuse the apiKey
   location and the app's manager wrapper; emit a diff. **Not found** → *scaffold
   minimally*: awaited `initWith`, plus the native `InAppStoryPlugin.initSDK` in
   `Application` and `MainActivity : InAppStoryActivity`. Pin every API to the
   detected version; return edits to real files, not a loose snippet — unless asked "how".
4. **Then** fetch the topic page and write against the live API.

## Verify a first integration

Only if the user opted in at Intake — the "yes" there is the go-ahead, so run
without re-asking. A first integration shouldn't be left untried.

- **Smoke-run:** `flutter run` on a booted emulator/simulator (`flutter devices`
  to confirm one). Watch the console for the feed's API call and cells appearing.
  → [how-to-get-started](https://docs.inappstory.com/sdk-guides/flutter/how-to-get-started)
- **Empty feed ≠ broken.** No cells can mean the integration is fine but the feed
  slug is wrong, the `apiKey` has no published stories, or the user is filtered out
  by tags. Confirm a successful API response in the console before assuming a bug.
- **Automated test (only if the user asked for one):** a `flutter test` widget
  smoke-check (the widget builds, no exception) is fine — don't assert on remote
  content, the feed loads live data and any content assertion will be flaky.
- **No emulator available?** Say so and give the user the exact run command; don't
  claim a pass you didn't see.

## Topics

### Getting started & core
| Topic | Page |
|---|---|
| How to get started | https://docs.inappstory.com/sdk-guides/flutter/how-to-get-started |
| InAppStoryManager (init & lifecycle) | https://docs.inappstory.com/sdk-guides/flutter/in-app-story-manager |
| Options | https://docs.inappstory.com/sdk-guides/flutter/options |
| User settings | https://docs.inappstory.com/sdk-guides/flutter/user-settings |
| Anonymous mode | https://docs.inappstory.com/sdk-guides/flutter/anonymous-mode |
| Migrations | https://docs.inappstory.com/sdk-guides/flutter/migrations |
| FAQ | https://docs.inappstory.com/sdk-guides/flutter/faq |

### Stories UI (feeds & lists)
| Topic | Page |
|---|---|
| FeedStoriesWidget | https://docs.inappstory.com/sdk-guides/flutter/feed-stories-widget |
| Single Story | https://docs.inappstory.com/sdk-guides/flutter/single-story |
| List Placeholders | https://docs.inappstory.com/sdk-guides/flutter/list-placeholders |
| Appearance | https://docs.inappstory.com/sdk-guides/flutter/appearance-manager |
| Banners place | https://docs.inappstory.com/sdk-guides/flutter/banners |

### Content types & features
| Topic | Page |
|---|---|
| Onboardings | https://docs.inappstory.com/sdk-guides/flutter/onboardings |
| In-App Messaging | https://docs.inappstory.com/sdk-guides/flutter/in-app-messaging |
| Games | https://docs.inappstory.com/sdk-guides/flutter/games |
| Goods | https://docs.inappstory.com/sdk-guides/flutter/goods |
| Checkout | https://docs.inappstory.com/sdk-guides/flutter/checkout |
| Favorites | https://docs.inappstory.com/sdk-guides/flutter/favorites |
| Call To Action | https://docs.inappstory.com/sdk-guides/flutter/call-to-action |
| Sound control | https://docs.inappstory.com/sdk-guides/flutter/sound-control |

### Targeting, events & handling
| Topic | Page |
|---|---|
| Tags | https://docs.inappstory.com/sdk-guides/flutter/tags |
| Events | https://docs.inappstory.com/sdk-guides/flutter/events |
| Cancellation of long-running actions | https://docs.inappstory.com/sdk-guides/flutter/cancellation-of-actions |

## Notes

- Full section index (may include topics added after this skill):
  https://docs.inappstory.com/sdk-guides/
- Other platforms have their own skills (`inappstory-android`, `inappstory-ios`,
  `inappstory-react-native`, `inappstory-react`, `inappstory-js`).
- `changelog` is intentionally omitted — fetch the base URL for version history.
