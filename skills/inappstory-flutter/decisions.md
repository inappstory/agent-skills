# Flutter IAS — decision guides

Choices the per-topic docs don't collect. Plugin `inappstory_plugin` (0.x).

## `MainActivity` base class — by plugin version

| Plugin version | Extend | Why |
|---|---|---|
| ≥ 0.7.1 | `InAppStoryActivity` | Back-button interception for IAM |
| 0.3.x–0.7.0 | `FlutterFragmentActivity` | required for IAM |
| < 0.3 | `FlutterActivity` | default |

On a modern version always use `InAppStoryActivity` — anything else breaks IAM
back-button handling.

## Calling the API — singleton vs old HostApi

- **Current (0.8.0+ / 0.11.0+):** everything via `InAppStoryManager.instance.…` /
  `AppearanceManager.instance.…`.
- If you see `IASSingleStoryHostApi()`, `IASInAppMessagesHostApi()`,
  `AppearanceManagerHostApi()`, `InAppStoryManagerHostApi()`, or `IASGamesHostApi()` (removed in 0.11.0)
  in a project, it's pre-migration code — rewrite to the singletons. See [pitfalls](pitfalls.md).

## Which list widget

- **`FeedStoriesWidget(feed:)`** — current, customizable.
- `getStoriesWidgets()` / `getFavoritesStoriesWidgets()` — deprecated, being
  removed. Don't add new code on them.

## Banners: Carousel (`BannerPlace`) vs Grid (`BannerGrid`)

- **`BannerPlace`**: horizontal scrolling carousel with `BannerPlaceDecoration` (`bannerOffset`, `bannersGap`, `cornerRadius`, `loop`).
- **`BannerGrid` (0.11.0+)**: two-column non-scrolling grid layout with `BannerGridDecoration` (`horizontalGap`, `verticalGap`, `cornerRadius`). Calculates full height and reports via `onBannerPlaceLoaded(size, widgetHeight)` — dynamically resize its container or wrap in a scroll view.

## Loading placeholders — global vs widget

- **0.11.0+**: Configure placeholders globally via `AppearanceManager.instance.setBannersPlaceholder(...)` and `AppearanceManager.instance.setStoriesPlaceholder(...)`. Per-widget `BannerDecoration` is deprecated and ignored.
- Platform note for banners: On iOS, `setBannersPlaceholder` applies to `BannerPlace` (grids show native cell loader); on Android, it applies to both carousel and grid.

## Single story & IAM targeting — direct vs withTargeting

- **`showStory` / `showIAMById`**: opens directly, bypassing targeting evaluation.
- **`showStoryWithTargeting` / `showIAMByIdWithTargeting` / `showIAMByEventWithTargeting` (0.11.0+)**: evaluates targeting rules before showing. Allows passing optional request-specific `tags` that override global tags for just that call without mutating global SDK state.

## Data models — Domain models vs generated DTOs

In ≥ 0.11.0, always use clean domain models (`StoryData`, `SlideData`, `InAppMessageData`, `GoodsItemData`, `ContentData`). Never import or reference generated `*Dto` classes (which are no longer exported).

## Callbacks — mixins

Implement the mixin, don't look for a delegate/HostApi callback:
`IASCallbacks`, `IASInAppMessageCallback`, `IASGameReaderCallback`,
`IASGoodItemSelectedCallback`, `IASCallToActionCallback`, `IASShowStoryCallback`,
`IASOnboardingLoadCallback`. In 0.11.0+, all callback parameters use domain models.
Banner events → callbacks on the `BannerPlace` / `BannerGrid` widget.

## cacheSize

Android-only (`CacheSize.small/medium/large`). No effect on iOS — don't rely on it
for cross-platform storage tuning.

_All pages under `https://docs.inappstory.com/sdk-guides/flutter/<name>`._
