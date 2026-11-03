# Changelog

All notable changes to **ias-agent-skills** are recorded here. Versions follow
[SemVer](https://semver.org). The version lives in `.claude-plugin/plugin.json`
and each release is tagged `vX.Y.Z` (cut with `scripts/release`).

## [Unreleased]

## [0.4.1]

- Sync the skill indexes and judgment layers with latest Android and iOS SDK docs:
  - **Android (1.26.0)**: document targeting by ID (`showStoryWithTargeting`,
    `InAppMessageOpenSettings.useTargeting()`), `BannerList` and `BannerGrid`
    widgets with lifecycle controls (`pauseBanners`/`resumeBanners`), nullable
    `AppearanceManager?`, 100-tag limit, and Jetpack Compose (`v1.1.26.0`)
    composables.
  - **iOS (1.29.9 / IASLottie 0.2.1)**: document targeting by ID
    (`showStoryWithTargeting`, `showInAppMessageWithTargeting`), `.verticalList`
    and `.tilesList` banner layouts with `pause()`/`resume()` controls, separate
    `placeholderIAMView` and `placeholderBannerView` loaders, input fields
    support, 100-tag limit, and updated `IASLottie` bridge.
  - Update `sync-docs.state` baseline.

## [0.4.0]

- Sync the skill indexes and judgment layers with the latest SDK docs:
  - **Flutter (0.10.0)**: document `ProductCartOffer.offerDescription` and
    `GoodsItemDataDto.productDescription` renames, iOS Swift Package Manager (SPM)
    support, `extraFields`, and the 100-tag limit.
  - **React Native (1.1.0)**: document programmatic reader closing via
    `storyManager.closeReaders()`, dynamic statistics toggle via
    `storyManager.setSendStatistics()`, `extraFields`, and the 100-tag limit.
  - **React & JS SDKs**: document user `targeting: true` and `signal` options
    for single story (`showStory`/`showStoryOnce`) and IAM (`showMessageById`),
    and `extraFields` payload attributes.
  - Update `sync-docs.state` baseline.

## [0.3.0]

- Sync the skill indexes and judgment layers with the latest SDK docs: add the
  legacy Android Compose, Flutter tags, and React Native Story Manager, Options,
  and product cart topics, plus their version and behavior caveats.
- Turn the **codebase-aware** step into an explicit write-integration procedure in
  all six skills: locate the existing setup by a concrete symbol → *extend* it
  (reuse the apiKey/serviceKey location, wrapper and language; emit a diff) or
  *scaffold minimally* in the app's own architecture → pin APIs to the detected SDK
  version → return edits to real files, not a loose snippet.
- Add **Reference integration** pointers to `inappstory-android` and
  `inappstory-ios` (the official example repos) with version caveats and a scope
  rule: borrow the SDK calls and their order, never the vanilla architecture — the
  target repo's structure (DI/MVVM/Compose/SwiftUI) always wins.
- Extend the **Intake** step to offer post-integration verification: on a first
  integration the agent now asks upfront (batched with the key / placement
  questions) whether to build & run the app afterwards to confirm the feed loads,
  and at what depth (smoke-run / optional smoke test / skip).
- Add a **Verify a first integration** section to each `inappstory-*` skill with
  the platform's run command, what to watch for, and the "empty feed ≠ broken"
  caveat. Automated tests stay opt-in and smoke-only (no assertions on live content).

## [0.2.0]

- Add a pre-integration **Intake** step to all six `inappstory-*` skills: the
  agent now asks for the integration key on a first integration and clarifies
  underspecified requests (where the UI goes / which feature) before writing code.

## [0.1.0]

- Initial release: six `inappstory-*` skills (Android, iOS, Flutter, React
  Native, React, JS) — live docs router plus curated playbooks/pitfalls/decisions.
