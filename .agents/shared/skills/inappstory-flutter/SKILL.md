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
| Events | https://docs.inappstory.com/sdk-guides/flutter/events |
| Cancellation of long-running actions | https://docs.inappstory.com/sdk-guides/flutter/cancellation-of-actions |

## Notes

- Full section index (may include topics added after this skill):
  https://docs.inappstory.com/sdk-guides/
- Other platforms have their own skills (`inappstory-android`, `inappstory-ios`,
  `inappstory-react-native`, `inappstory-react`, `inappstory-js`).
- `changelog` is intentionally omitted — fetch the base URL for version history.
