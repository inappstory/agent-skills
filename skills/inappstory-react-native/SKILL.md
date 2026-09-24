---
name: inappstory-react-native
description: "Integrate and use the InAppStory (IAS) SDK on React Native — StoryManager, stories list, in-app messaging, games, goods, banners, favorites, appearance, events, and more. Use when adding, configuring, or debugging the InAppStory React Native module, or answering how the RN IAS SDK works."
---

<!--
Vendor-neutral: no `allowed-tools` on purpose. Routes to the public docs and
expects the host agent to fetch a URL (Claude: WebFetch; others: a browser/fetch
tool). Agents without a fetch tool degrade gracefully — the URLs are clickable.
argument-hint: [topic, e.g. stories-list, in-app-messaging, appearance]
-->

# InAppStory SDK — React Native

This skill routes to the **official InAppStory React Native docs**. The docs are
the source of truth and change often, so this skill does not copy them — it
points to the exact page and expects you to **fetch it on demand**.

## How to use

1. Find the relevant topic in the index below.
2. **Fetch that page** (`WebFetch <url>`) and answer from the live content —
   never guess SDK APIs, versions, or npm coordinates from memory.
3. New to the SDK? Start with **How to get started**.
4. If you have no fetch tool, give the user the exact URL to open.

Base URL: `https://docs.inappstory.com/sdk-guides/react-native/`

## Judgment layer (read these first — what a doc page won't tell you)

- **[playbooks.md](playbooks.md)** — end-to-end recipes incl. the mandatory native
  host setup (iOS static frameworks, Android `initSDK` + `InAppStoryActivity` +
  manifest), CodePush version override.
- **[pitfalls.md](pitfalls.md)** — grounded gotchas: static-frameworks Podfile,
  `initSDK(this as Application)` form (0.28+), `MainActivity : InAppStoryActivity`
  + `enableOnBackInvokedCallback` (0.27+), legacy-SDK font/svgMask breaks.
- **[decisions.md](decisions.md)** — base class & `initSDK` form by version, app-
  version source (CodePush), where the docs are thin (fall back to native pages).

## Intake — ask before you write

Two quick checks before any integration work:

1. **Underspecified request? Ask, don't guess.** If the user didn't say *where*
   the UI goes (which screen/component) or *which* feature they mean, ask before
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

1. **Check the package version** in `package.json`
   (`@inappstory/react-native-sdk`); if absent, ask. Native init changed at 0.27
   and 0.28 — answer for that version, fetch **migrations** for deltas.
2. **Verify the native host setup** — iOS static frameworks, and Android
   `MainApplication.initSDK` / `MainActivity : InAppStoryActivity` / manifest flag.
   Most Android failures are here, not in JS.
3. **Write against the repo, not a blank slate (codebase-aware).** Grep for
   `new StoryManager(` / `StoryManagerConfig` / `InAppStory.initSDK` and
   `@inappstory/react-native-sdk` in `package.json`. **Found** → *extend* it: reuse
   the config/wrapper and apiKey location; emit a diff. **Not found** → *scaffold
   minimally* in the app's conventions, incl. the native `MainApplication.initSDK`
   and `MainActivity : InAppStoryActivity`. Pin every API to the detected version;
   return edits to real files, not a loose snippet — unless asked "how".
4. **Then** fetch the topic page and write against the live API.

## Verify a first integration

Only if the user opted in at Intake — the "yes" there is the go-ahead, so run
without re-asking. A first integration shouldn't be left untried.

- **Smoke-run:** `npx react-native run-android` / `run-ios` (Metro starts
  automatically) on a booted emulator/simulator. Watch the Metro + native logs for
  the feed's API call and cells appearing.
  → [how-to-get-started](https://docs.inappstory.com/sdk-guides/react-native/how-to-get-started)
- **Empty feed ≠ broken.** No cells can mean the integration is fine but the feed
  slug is wrong, the `apiKey` has no published stories, or the user is filtered out
  by tags. Confirm a successful API response in the logs before assuming a bug.
- **Automated test (only if the user asked for one):** keep it a smoke/render check
  (the component mounts, no error thrown), not an assertion on remote content — the
  feed loads live data, so any content assertion will be flaky.
- **No emulator available?** Say so and give the user the exact run command; don't
  claim a pass you didn't see.

## Topics

### Getting started & core
| Topic | Page |
|---|---|
| How to get started | https://docs.inappstory.com/sdk-guides/react-native/how-to-get-started |
| Story Manager | https://docs.inappstory.com/sdk-guides/react-native/story-manager |
| Options | https://docs.inappstory.com/sdk-guides/react-native/options |
| User settings | https://docs.inappstory.com/sdk-guides/react-native/user-settings |
| Migrations | https://docs.inappstory.com/sdk-guides/react-native/migrations |

### Stories UI (feeds & lists)
| Topic | Page |
|---|---|
| Stories List | https://docs.inappstory.com/sdk-guides/react-native/stories-list |
| Placeholders | https://docs.inappstory.com/sdk-guides/react-native/placeholders |
| Appearance | https://docs.inappstory.com/sdk-guides/react-native/appearance |
| Banners place | https://docs.inappstory.com/sdk-guides/react-native/banners |

### Content types & features
| Topic | Page |
|---|---|
| In-App Messaging | https://docs.inappstory.com/sdk-guides/react-native/in-app-messaging |
| Games | https://docs.inappstory.com/sdk-guides/react-native/games |
| Goods | https://docs.inappstory.com/sdk-guides/react-native/goods |
| Product cart | https://docs.inappstory.com/sdk-guides/react-native/product-cart |
| Call To Action | https://docs.inappstory.com/sdk-guides/react-native/call-to-action |
| Favorites | https://docs.inappstory.com/sdk-guides/react-native/favorites |
| Sound | https://docs.inappstory.com/sdk-guides/react-native/sound |

### Targeting, events & handling
| Topic | Page |
|---|---|
| Events | https://docs.inappstory.com/sdk-guides/react-native/events |
| Tags | https://docs.inappstory.com/sdk-guides/react-native/tags |
| Cancellation of actions | https://docs.inappstory.com/sdk-guides/react-native/cancellation-of-actions |

## Notes

- Full section index (may include topics added after this skill):
  https://docs.inappstory.com/sdk-guides/
- Other platforms have their own skills (`inappstory-android`, `inappstory-ios`,
  `inappstory-flutter`, `inappstory-react`, `inappstory-js`).
- `changelog` is intentionally omitted — fetch the base URL for version history.
