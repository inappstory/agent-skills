# Flutter IAS — task playbooks

Recipes across pages. Plugin `inappstory_plugin` (0.x). Verify the version in
`pubspec.yaml`; read [pitfalls](pitfalls.md) alongside — the native Android setup
is the usual failure point.

Before any recipe, run the **Intake** (SKILL.md): clarify an underspecified
request (*where* / *which* feature), and on a first integration ask the user for
their integration key (`apiKey`). After a first integration, offer to
verify it runs (see **Verify a first integration** in SKILL.md).

## Add a stories feed (first-time integration)

1. **Add the dep:** `flutter pub add inappstory_plugin` (or pin in `pubspec.yaml`).
2. **Android native (mandatory):**
   - `app/build.gradle`: `minSdkVersion = 23`, compile/target 34, and
     `manifestPlaceholders['applicationName'] = '<your Application class>'`.
   - In your `Application.onCreate()`: `InAppStoryPlugin.initSDK(this)`.
   - `MainActivity` extends `InAppStoryActivity` (not `FlutterActivity`).
3. **iOS native:** `pod install` in `ios/` (or use Swift Package Manager with Flutter 3.24+).
4. **Init (Dart, async):** `await InAppStoryPlugin().initWith('<apiKey>', '<userId>',
   locale:, cacheSize: CacheSize.medium)`.
5. **Show the feed:** put `FeedStoriesWidget(feed: '<feedId>')` in the tree, gated
   behind the init `Future` (e.g. `FutureBuilder`).
   → [how-to-get-started](https://docs.inappstory.com/sdk-guides/flutter/how-to-get-started),
   [feed-stories-widget](https://docs.inappstory.com/sdk-guides/flutter/feed-stories-widget)

## Show onboardings / single story / IAM / games (0.8.0+ / 0.11.0+)

All go through the `InAppStoryManager.instance` singleton:
- Onboardings: `InAppStoryManager.instance.showOnboardings(limit)`.
  → [onboardings](https://docs.inappstory.com/sdk-guides/flutter/onboardings)
- Single story: `showStory(storyId)` / `showStoryOnce(storyId)` (bypasses targeting),
  or `showStoryWithTargeting(storyId, tags: ...)` (0.11.0+) to evaluate targeting rules
  with optional request-specific tags.
  → [single-story](https://docs.inappstory.com/sdk-guides/flutter/single-story)
- In-App Messaging: `showIAMById(id)` / `showIAMByEvent(event)` / `preloadInAppMessages()`.
  In 0.11.0+, use `showIAMByIdWithTargeting(id, tags: ...)` or `showIAMByEventWithTargeting(event, tags: ...)`
  to evaluate targeting and pass request-specific tags. Requires the `InAppStoryActivity`
  back-button setup.
  → [in-app-messaging](https://docs.inappstory.com/sdk-guides/flutter/in-app-messaging)
- Games: `openGame(gameId)`, `closeGame()`, and `preloadGames()` (0.11.0+;
  `IASGamesHostApi` is removed).
  → [games](https://docs.inappstory.com/sdk-guides/flutter/games)

## Change user / appearance / placeholders

- Switch user: `InAppStoryManager.instance.changeUser('<newUserId>')`.
  → [in-app-story-manager](https://docs.inappstory.com/sdk-guides/flutter/in-app-story-manager),
  [user-settings](https://docs.inappstory.com/sdk-guides/flutter/user-settings)
- Appearance: `AppearanceManager.instance.…` (singleton since 0.4.0).
  → [appearance-manager](https://docs.inappstory.com/sdk-guides/flutter/appearance-manager)
- Global placeholders (0.11.0+): configure once globally via
  `AppearanceManager.instance.setStoriesPlaceholder(decoration: ...)` for story covers and
  `AppearanceManager.instance.setBannersPlaceholder(decoration: ...)` for banner content.
  → [appearance-manager](https://docs.inappstory.com/sdk-guides/flutter/appearance-manager),
  [list-placeholders](https://docs.inappstory.com/sdk-guides/flutter/list-placeholders)
- Android navigation bar color (0.11.0+):
  `AppearanceManager.instance.setNavBarColor(Colors.black, darkColor: Colors.black)`.

## Add banners (carousel & grid)

- **Carousel:** `BannerPlace(placeId:, height:, placeDecoration: BannerPlaceDecoration(...), onBannerScroll: (i){…})`.
- **Grid (0.11.0+):** `BannerGrid(placeId:, height:, gridDecoration: BannerGridDecoration(horizontalGap: 8, verticalGap: 8, cornerRadius: 16), onBannerPlaceLoaded: (size, widgetHeight){…})` — 2-column non-scrolling grid layout. Resize dynamically using the calculated `widgetHeight` or wrap in a scroll view.
- Note: `BannerDecoration` and `BannerPlace.bannerDecoration` are deprecated in 0.11.0 (ignored). Use `AppearanceManager.instance.setBannersPlaceholder(...)`.
  → [banners](https://docs.inappstory.com/sdk-guides/flutter/banners)

## Update user tags

- Keep tags to letters, numbers, `_`, and `-`; maximum 100 tags in the list.
- `setTags` replaces the full list; `addTags` and `removeTags` update it.
- After changing tags, reload the `FeedStoriesController` so the feed reflects
  the new targeting.
  → [tags](https://docs.inappstory.com/sdk-guides/flutter/tags)
