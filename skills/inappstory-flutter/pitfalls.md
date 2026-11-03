# Flutter IAS — pitfalls & version traps

Distilled from get-started / migrations. Plugin: `inappstory_plugin` (0.x
versions). Check the version in `pubspec.yaml` and fetch
[migrations](https://docs.inappstory.com/sdk-guides/flutter/migrations) for deltas.

## Native setup is mandatory (this is where it silently fails)

The Dart package alone is **not enough** — you must touch the native Android host:
- **`InAppStoryPlugin.initSDK(this)` in your `Application` class.** The docs warn:
  *without this the library will not work on Android at all.* Register the custom
  Application via `manifestPlaceholders['applicationName']` in `app/build.gradle`.
- **`MainActivity` must extend `InAppStoryActivity`** (since 0.7.1), not
  `FlutterActivity`/`FlutterFragmentActivity`. It intercepts the hardware **Back**
  button so IAM closes correctly. Wrong base class → Back bypasses the SDK and the
  reader won't close. (History: `FlutterActivity` → `FlutterFragmentActivity` for
  IAM in 0.3 → `InAppStoryActivity` in 0.7.1.)
- **Android** `minSdkVersion = 23`, compile/target 34.
- **iOS**: run `pod install` (or `--repo-update`) in the `ios/` folder, or use Swift Package Manager (SPM, supported natively in Flutter 3.24+).

## Init is async — await it

- `await InAppStoryPlugin().initWith('<apiKey>', '<userId>', locale:, cacheSize:)`
  **before any other API call.** In UI, gate the widget behind the init `Future`
  (e.g. `FutureBuilder`) — using `FeedStoriesWidget` before init resolves fails.
- `userId` can be empty. `locale` needs a region subtag (`Locale('en','US')`) or
  it defaults to en-US. `cacheSize` is **Android-only** (small 15 / medium 110 /
  large 210 MB; medium default).

## Singletons — use `.instance` (post-migration)

- `InAppStoryManager` is a singleton since **0.3.4** → `InAppStoryManager.instance.…`
  (not `InAppStoryManagerHostApi()`).
- `AppearanceManager` is a singleton since **0.4.0** → `AppearanceManager.instance.…`.
- **0.8.0 rename:** call `InAppStoryManager.instance.showStory/showStoryOnce/
  showIAMById/showIAMByEvent/preloadInAppMessages/showOnboardings(...)` — the old
  `IASSingleStoryHostApi()/IASInAppMessagesHostApi()/IASOnboardingsHostApi()` forms
  are gone. Also brought cancellation of long-running ops.
- **0.11.0 games:** `IASGamesHostApi` is removed — call `InAppStoryManager.instance.openGame()`,
  `closeGame()`, and `preloadGames()`.

## Widgets & callbacks

- **`FeedStoriesWidget` is the current list widget** (since 0.3.x). The old
  `InAppStoryPlugin().getStoriesWidgets()` / `getFavoritesStoriesWidgets()` are
  deprecated and being removed.
- Callbacks moved to **mixins**: `IASCallbacks`, `IASInAppMessageCallback`,
  `IASGameReaderCallback`, `IASGoodItemSelectedCallback`, `IASCallToActionCallback`,
  `IASShowStoryCallback`, `IASOnboardingLoadCallback`. In 0.11.0+, all callback
  signatures use domain models (`StoryData`, `SlideData`, `InAppMessageData`,
  `GoodsItemData`, `ContentData`) instead of `*Dto` classes.
- **Goods callback (0.11.0):** `IASGoodItemSelectedCallback` receives `GoodsItemData item`
  where the description property is `item.description` (reverting the 0.10.0 `productDescription` rename).
- **Banner events**: the `IASBannerPlaceCallback` mixin was **removed in 0.7.6** —
  listen via callbacks on the `BannerPlace` / `BannerGrid` widget itself (`onBannerScroll`, `onBannerPlaceLoaded`).

## Tags replace versus mutate

- Invalid tags clear the list when passed to `setTags`.
- Invalid tags are ignored by `addTags` and `removeTags`.
- **Validation limit (0.10.0+):** max 100 tags (previous 3999-byte limit was replaced). Allowed characters: letters, digits, `_`, `-`.
- **Targeting tags override (0.11.0+):** `showStoryWithTargeting(id, tags: [...])`, `showIAMByIdWithTargeting(id, tags: [...])`, and `showIAMByEventWithTargeting(event, tags: [...])` accept request-specific tags that override active tags for that single evaluation without modifying global SDK tags.

## Migrating to 0.11.0 (domain models, game controls, targeting & banner grid)

- **Domain models replace generated DTOs**: `StoryData`, `SlideData`, `InAppMessageData`,
  `GoodsItemData`, `ContentData`, `StoryType`, `SourceType`, `ClickAction`, `InAppMessageType`,
  `ContentType`, and `PlaceholderDecoration` replace `*Dto` classes throughout the public API.
  Pigeon DTO classes are no longer exported.
- **Goods**: `GoodsItemData.description` is used to access product description (replaces `productDescription` from 0.10.0). `setGetSkusCallback` returns `Future<List<GoodsItemData>>`.
- **Game controls**: `IASGamesHostApi` is no longer exported; use `InAppStoryManager.instance.openGame(gameId)`, `closeGame()`, and `preloadGames()`.
- **Targeting**: `showStoryWithTargeting(storyId, tags:)`, `showIAMByIdWithTargeting(id, tags:)`, and `showIAMByEventWithTargeting(event, tags:)` evaluate targeting and support request-specific tags. `showStory` and `showIAMById` skip targeting.
- **Banners**: `BannerGrid` widget for two-column grid layouts. `BannerDecoration` and `BannerPlace.bannerDecoration` are deprecated and ignored; configure loading placeholders globally via `AppearanceManager.instance.setBannersPlaceholder()`. Story covers support `AppearanceManager.instance.setStoriesPlaceholder()`.

## Migrating to 0.10.0 (breaking renames & extraFields)

- **`ProductCartOffer`**: `description` field was renamed to `offerDescription`.
- **`GoodsItemDataDto`**: `description` field in `goodsItemSelected` callback was renamed to `productDescription` (superceded by `GoodsItemData.description` in 0.11.0).
- **`extraFields`**: `Map<String, String>? extraFields` is now available on `StoryData`, `InAppMessageData`, and `BannerData`.
