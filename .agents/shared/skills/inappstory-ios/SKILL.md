---
name: inappstory-ios
description: "Integrate and use the InAppStory (IAS) SDK on iOS — stories feeds (StoryView/UIKit, StoryListView/SwiftUI), single stories, onboardings, in-app messaging, games, banners, favorites, appearance, events, and more. Use when adding, configuring, or debugging InAppStory on iOS in Swift (UIKit or SwiftUI), or answering how the iOS IAS SDK works."
---

<!--
Vendor-neutral: no `allowed-tools` on purpose. Routes to the public docs and
expects the host agent to fetch a URL (Claude: WebFetch; others: a browser/fetch
tool). Agents without a fetch tool degrade gracefully — the URLs are clickable.
argument-hint: [topic, e.g. story-view, in-app-messaging, appearance]
-->

# InAppStory SDK — iOS

This skill routes to the **official InAppStory iOS docs**. The docs are the
source of truth and change often, so this skill does not copy them — it points
to the exact page and expects you to **fetch it on demand**.

## How to use

1. Find the relevant topic in the index below.
2. **Fetch that page** (`WebFetch <url>`) and answer from the live content —
   never guess SDK APIs, versions, or CocoaPods/SPM coordinates from memory.
3. New to the SDK? Start with **How to get started**, then **InAppStory class**
   and **Options**.
4. If you have no fetch tool, give the user the exact URL to open.

Base URL: `https://docs.inappstory.com/sdk-guides/ios/`

## Topics

### Getting started & core
| Topic | Page |
|---|---|
| How to get started | https://docs.inappstory.com/sdk-guides/ios/how-to-get-started |
| InAppStory class (init & lifecycle) | https://docs.inappstory.com/sdk-guides/ios/inappstory |
| Options | https://docs.inappstory.com/sdk-guides/ios/options |
| User settings | https://docs.inappstory.com/sdk-guides/ios/user-settings |
| Anonymous mode | https://docs.inappstory.com/sdk-guides/ios/anonymous-mode |
| API reference | https://docs.inappstory.com/sdk-guides/ios/reference |
| Migrations | https://docs.inappstory.com/sdk-guides/ios/migrations |

### Stories UI (feeds & lists)
| Topic | Page |
|---|---|
| StoryView (UIKit) | https://docs.inappstory.com/sdk-guides/ios/story-view |
| StoryListView (SwiftUI) | https://docs.inappstory.com/sdk-guides/ios/story-list-view |
| Single Story | https://docs.inappstory.com/sdk-guides/ios/single-story |
| Multi-feed | https://docs.inappstory.com/sdk-guides/ios/multi-feed |
| Stack Feed | https://docs.inappstory.com/sdk-guides/ios/stack-feed |
| Home Screen Widget | https://docs.inappstory.com/sdk-guides/ios/home-screen-widget |
| List Placeholder (skeleton) | https://docs.inappstory.com/sdk-guides/ios/list-placeholder |
| Placeholders | https://docs.inappstory.com/sdk-guides/ios/placeholders |
| Appearance | https://docs.inappstory.com/sdk-guides/ios/appearance |
| Screen presenting | https://docs.inappstory.com/sdk-guides/ios/screen-presenting |
| Refresh | https://docs.inappstory.com/sdk-guides/ios/refresh |
| Tracking coverage (visible update) | https://docs.inappstory.com/sdk-guides/ios/visible-update |

### Content types & features
| Topic | Page |
|---|---|
| Onboardings | https://docs.inappstory.com/sdk-guides/ios/onboardings |
| In-App Messaging | https://docs.inappstory.com/sdk-guides/ios/in-app-messaging |
| In-App Messaging (>1.28.0) | https://docs.inappstory.com/sdk-guides/ios/in-app-messaging-v2 |
| In-App Messaging examples (SwiftUI) | https://docs.inappstory.com/sdk-guides/ios/in-app-messaging-examples-swiftui |
| In-App Messaging examples (UIKit) | https://docs.inappstory.com/sdk-guides/ios/in-app-messaging-examples-uikit |
| Games | https://docs.inappstory.com/sdk-guides/ios/games |
| Banners place | https://docs.inappstory.com/sdk-guides/ios/banners |
| Widget "Goods" | https://docs.inappstory.com/sdk-guides/ios/widget-goods |
| Checkout | https://docs.inappstory.com/sdk-guides/ios/checkout |
| Likes, Share, Favorites | https://docs.inappstory.com/sdk-guides/ios/favorites |
| Lottie animation | https://docs.inappstory.com/sdk-guides/ios/lottie-animation |
| Sound control | https://docs.inappstory.com/sdk-guides/ios/sound-control |

### Targeting, events & handling
| Topic | Page |
|---|---|
| Tags | https://docs.inappstory.com/sdk-guides/ios/tags |
| Events | https://docs.inappstory.com/sdk-guides/ios/events |
| Link handling | https://docs.inappstory.com/sdk-guides/ios/link-handling |
| Cancellation of long-running actions | https://docs.inappstory.com/sdk-guides/ios/cancellation-of-actions |
| Notifications | https://docs.inappstory.com/sdk-guides/ios/notifications |

### Advanced & platform
| Topic | Page |
|---|---|
| SSL Pinning | https://docs.inappstory.com/sdk-guides/ios/ssl-pinning |
| FilePicker | https://docs.inappstory.com/sdk-guides/ios/file-picker |
| Custom logging | https://docs.inappstory.com/sdk-guides/ios/custom-logging |

## Notes

- Full section index (may include topics added after this skill):
  https://docs.inappstory.com/sdk-guides/
- Other platforms have their own skills (`inappstory-android`,
  `inappstory-flutter`, `inappstory-react-native`, `inappstory-react`,
  `inappstory-js`).
- `changelog` is intentionally omitted — fetch the base URL for version history.
