# JS SDK IAS — task playbooks

Recipes across pages. Package `@inappstory/js-sdk` (3.x). Verify the version
(`package.json` or CDN URL); read [pitfalls](pitfalls.md) alongside.

Before any recipe, run the **Intake** (SKILL.md): clarify an underspecified
request (*where* / *which* feature), and on a first integration ask the user for
their integration key (`apiKey`). After a first integration, offer to
verify it runs (see **Verify a first integration** in SKILL.md).

## Add a stories list

### NPM
1. `npm install @inappstory/js-sdk`.
2. `import { InAppStoryManager, AppearanceManager } from "@inappstory/js-sdk"`.
3. Put `<div id="stories_widget"></div>` in the markup.
4. ```ts
   const inAppStoryManager = new InAppStoryManager({ apiKey: "{key}", userId: "{id}" });
   const appearanceManager = new AppearanceManager();
   const storiesList = new inAppStoryManager.StoriesList(
     "#stories_widget", appearanceManager, { feed: "default" });
   ```

### CDN
Same, but load `IAS.js`, run inside `DOMContentLoaded`, and use
`window.IAS.InAppStoryManager` / `window.IAS.AppearanceManager`.

→ [how-to-get-started](https://docs.inappstory.com/sdk-guides/js-sdk/how-to-get-started),
[feeds](https://docs.inappstory.com/sdk-guides/js-sdk/feeds),
[story-view](https://docs.inappstory.com/sdk-guides/js-sdk/story-view)

## Subscribe to events

```ts
["clickOnStory","showStory","closeStory","clickOnButton","likeStory",
 "favoriteStory","shareStory","feedLoad","feedImpression"]
 .forEach(e => inAppStoryManager.on(e, p => console.log(e, p)));
```
→ [events](https://docs.inappstory.com/sdk-guides/js-sdk/events)

## Feature entry points

- Onboarding → [onboardings](https://docs.inappstory.com/sdk-guides/js-sdk/onboardings)
- Single story: `inAppStoryManager.showStory(id, { targeting: true, signal })` / `showStoryOnce(id, { targeting: true, signal })` —
  `targeting: true` (since 3.15.8) applies user targeting on fetch; pass `signal: AbortSignal` to cancel.
  → [single-story](https://docs.inappstory.com/sdk-guides/js-sdk/single-story),
  [external-api](https://docs.inappstory.com/sdk-guides/js-sdk/external-api)
- In-App Messaging: `inAppMessaging.showMessageById(id, { targeting: true })` — set `targeting: true`
  (since 3.15.8) to apply user targeting.
  → [in-app-messaging](https://docs.inappstory.com/sdk-guides/js-sdk/in-app-messaging)
- Events & extra fields: `extraFields` attribute is provided on Stories, IAM, and Banners payloads.
  → [events](https://docs.inappstory.com/sdk-guides/js-sdk/events)
- Stack feed → [stack-feed](https://docs.inappstory.com/sdk-guides/js-sdk/stack-feed),
  Goods → [widget-goods](https://docs.inappstory.com/sdk-guides/js-sdk/widget-goods),
  Games → [games](https://docs.inappstory.com/sdk-guides/js-sdk/games)

## Personalize

`userId`, `userIdSign` (if console requires signing), `tags`, `placeholders`,
`imagePlaceholders`, `lang`, `dir` — all in the manager config.
→ [user-settings](https://docs.inappstory.com/sdk-guides/js-sdk/user-settings),
[tags](https://docs.inappstory.com/sdk-guides/js-sdk/tags)

## Deploying under a CSP

Apply the SDK's required CSP directives before assuming a render bug.
→ [implement-content-security-policies](https://docs.inappstory.com/sdk-guides/js-sdk/implement-content-security-policies)
