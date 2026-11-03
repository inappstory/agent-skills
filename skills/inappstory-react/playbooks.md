# React IAS — task playbooks

Recipes across pages. Package `@inappstory/react-sdk`. Verify the version in
`package.json`; read [pitfalls](pitfalls.md) alongside.

Before any recipe, run the **Intake** (SKILL.md): clarify an underspecified
request (*where* / *which* feature), and on a first integration ask the user for
their integration key (`apiKey`). After a first integration, offer to
verify it runs (see **Verify a first integration** in SKILL.md).

## Add a stories list

1. **Install:** `npm install @inappstory/react-sdk`.
2. **Options module** (`inAppStoryOptions.ts`): export `commonOptions`
   (`hasShare/hasLike/hasFavorite`), `storiesListOptions`, `storyReaderOptions`.
3. **Wrap + render:**
   ```tsx
   <IASContainer config={{ apiKey: "{projectToken}" }}
                 commonOptions={commonOptions}
                 storyReaderOptions={storyReaderOptions}
                 onClickOnStory={handler}>
     <StoryList options={storiesListOptions} feedSlug="default" hasFavorite={false} />
   </IASContainer>
   ```
   → [how-to-get-started](https://docs.inappstory.com/sdk-guides/react-sdk/how-to-get-started),
   [feeds](https://docs.inappstory.com/sdk-guides/react-sdk/feeds),
   [story-view](https://docs.inappstory.com/sdk-guides/react-sdk/story-view)

## Feature entry points

- Onboarding → [onboardings](https://docs.inappstory.com/sdk-guides/react-sdk/onboardings)
- Single story: `showStory(id, { targeting: true, signal })` / `showStoryOnce(id, { targeting: true, signal })` —
  set `targeting: true` (since 1.16.9) to apply user targeting on fetch; pass `signal: AbortSignal` to cancel.
  → [single-story](https://docs.inappstory.com/sdk-guides/react-sdk/single-story),
  [external-api](https://docs.inappstory.com/sdk-guides/react-sdk/external-api)
- In-App Messaging: `inAppMessaging.showMessageById(id, { targeting: true })` — set `targeting: true`
  (since 1.16.9) to apply user targeting.
  → [in-app-messaging](https://docs.inappstory.com/sdk-guides/react-sdk/in-app-messaging)
- Events & extra fields: `extraFields` attribute is provided on Stories, IAM, and Banners payloads.
  → [events](https://docs.inappstory.com/sdk-guides/react-sdk/events)
- Games → [games](https://docs.inappstory.com/sdk-guides/react-sdk/games),
  Favorites → [favorites](https://docs.inappstory.com/sdk-guides/react-sdk/favorites),
  Share panel → [share-panel](https://docs.inappstory.com/sdk-guides/react-sdk/share-panel)

## Personalize (userId / tags / placeholders)

Pass through `StoryManagerConfig`: `userId`, `userIdSign` (if console requires
signing), `tags`, `placeholders`, `imagePlaceholders`, `lang`, `dir`.
→ [user-settings](https://docs.inappstory.com/sdk-guides/react-sdk/user-settings),
[tags](https://docs.inappstory.com/sdk-guides/react-sdk/tags),
[placeholders](https://docs.inappstory.com/sdk-guides/react-sdk/placeholders)

## Deploying under a CSP

If the app sends a Content-Security-Policy, apply the SDK's required directives
first — otherwise widgets silently fail to render.
→ [implement-content-security-policies](https://docs.inappstory.com/sdk-guides/react-sdk/implement-content-security-policies)
