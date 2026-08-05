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

## Topics

### Getting started & core
| Topic | Page |
|---|---|
| How to get started | https://docs.inappstory.com/sdk-guides/react-native/how-to-get-started |
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
