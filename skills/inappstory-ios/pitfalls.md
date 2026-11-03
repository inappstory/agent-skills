# iOS IAS — pitfalls & version traps

Distilled from the docs' get-started / migrations / reference pages. **Two things
dominate iOS: the UIKit-vs-SwiftUI split and the delegate→closure migration.**
Every item is version-gated — check the app's SDK version first (grep `Podfile` /
`Package.swift` / `Cartfile` for the `inappstory` dependency tag) and fetch
[migrations](https://docs.inappstory.com/sdk-guides/ios/migrations) for exact deltas.

## UIKit vs SwiftUI — they are different products

- **Different dependency, module, and min-iOS.** UIKit: pod/package `InAppStory`,
  `import InAppStorySDK`, iOS ≥ 11. SwiftUI: `InAppStory_SwiftUI`, tag suffix
  `-SwiftUI` (e.g. `1.29.2-SwiftUI`), `import InAppStorySDK_SwiftUI`, iOS ≥ 13.
  Picking the wrong pod/module/tag is the #1 setup failure. Decide upfront.
- **Different list class**: `StoryView` (UIKit, a `UIView` you frame + `addSubview`
  + `.create()`) vs `StoryListView` (SwiftUI view). Don't mix guides.
- SwiftUI without an `AppDelegate`: init via `@UIApplicationDelegateAdaptor`.

## Action handling changed API twice — this is the biggest trap

Which mechanism is correct depends entirely on version:
- **≤ 1.21.x — delegates.** `InAppStoryDelegate` set on `storyView.storiesDelegate`
  before `.create()`.
- **1.22.x — closures (delegates deprecated).** `InAppStory.shared.storiesDidUpdated`
  / `.onActionWith`, or per-list `storyView.storiesDidUpdated` / `.onActionWith`
  (per-list overrides global). SwiftUI: `.onUpdate/.onAction/.onDismiss` modifiers.
- **≥ 1.23.0 — delegates REMOVED.** `InAppStoryDelegate`,
  `StoryViewDelegateFlowLayout`, `GoodsDelegateFlowLayout` are unavailable; you
  *must* use closures. NotificationCenter events are deprecated too → subscribe
  `InAppStory.shared.storiesEvent` / `.gameEvent` / `.failureEvent`
  (`IASEvent.*`) instead.

If you see `InAppStoryDelegate` in a modern project, it won't compile on ≥1.23.

## StoryView lifecycle (UIKit)

- **Call `.create()`** after `addSubview` — nothing loads until you do.
- **Set delegate/closures and per-list params *before* `.create()`.**
- Close any reader from anywhere: `InAppStory.shared.closeReader(complete:)`
  (1.23+ closes *any* open reader; `complete` fires even if none was open).
  `closeReader` was removed from `StoryView` in 1.11.

## Settings limits (1.21+)

- `userID` ≤ **255 bytes**. `tags` limit changed in 1.29.6+ to a **maximum of 100 tags**
  (previously 4000 bytes). Exceeding a limit prints to the IDE console and **the SDK stops working**
  — validate before assigning.
- `userID`/`tags` can be omitted at `initWith(serviceKey:)` and set later via
  `InAppStory.shared.settings = Settings(userID:tags:)` **before** creating the list.

## Bottom panel (likes/favorites/share)

- **`panelSettings: PanelSettings` since 1.16** merged the old `likePanel` /
  `favoritePanel` / `sharePanel` bools — those are removed. Reactions must also be
  **enabled in the console**, or the panel won't show regardless of code.

## List direction & cell sizing (1.21+)

- `direction` added: list default `horizontal(rows: 1)`, favorites
  `vertical(columns: 3)`. **Cell size is derived from list size ÷ rows/columns** —
  change `direction` and cells can become tiny or huge. Default cell is a **square**
  (1:1), stroke 1pt; aspect ratio otherwise comes from the console.

## In-App Messaging 1.28 breaking change

- **`inAppMessageWillShow` signature changed.** A zero-arg closure `{ … }` **won't
  compile** on 1.28. New form: `{ id, event, presentType in … return nil }`
  returning `UIView?` (new enum `IAMPresentType`: `.fullScreen/.bottomSheet/.popUp/.toast`).
- `showInAppMessageWith(id:/event:)` gained optional `targetView: UIView? = nil`.
  Container priority: view from `inAppMessageWillShow` → `targetView` → default
  container (SwiftUI `.inAppMessageContainer()`). Old no-container calls still valid.
- `inAppMessageDidClose` unchanged. See in-app-messaging-v2.

## Renames that break older code

- **Goods (1.22):** `discount`→`oldPrice` (and its `init`), `goodsCloseBackgroundColor`
  → `goodsSubstrateColor`, `goodsCellDiscountTextColor`→`goodsCellOldPriceTextColor`.
- **Show methods (1.22 rename, earlier):** `showSingleStory`→`showSingle`,
  `showOnboarding`→`showOnboardings`; `storyView.delegate`→`storiesDelegate`.
- **Modal over reader (1.22):** the per-reader present methods merged into one
  `present(controller:for:with:)`.
- **openGame re-entry (1.23):** calling `openGame` while a game is open does nothing;
  `complete` returns `opened == false` and `gameEvent` gets `.gameFailure`.
- **Targeting by ID (1.29.9):** `showStoryWithTargeting` and `showInAppMessageWithTargeting`
  enable targeting filters when requesting content by ID.
- **Separate IAM / banner placeholders (1.29.9):** `placeholderIAMView` and
  `placeholderBannerView` in `Appearance` customize IAM and banner loaders independently.
- **Banner layouts & lifecycle (1.29.9):** `.verticalList` (internal scroll) and
  `.tilesList` (2-column grid, external scroll) layouts added with `pause()` and `resume()`
  controls in UIKit and SwiftUI.
- **Input fields (1.29.9):** IAM, banners, and games support text, email, and telephone
  inputs with optional custom `InputPresenter`.
- **Lottie bridge (0.2.1):** `IASLottie` requires `airbnb/lottie-ios` >= 4.6.1.
- **Extra fields (1.29.7):** `extraFields: [String: String]` on `StoryData`,
  `InAppMessageData`, and `IASBannerData`.
