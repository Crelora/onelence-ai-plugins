---
name: install-tracking
description: Installs OneLence tracking (the @crelora/mark SDK) in the website or app in the current codebase. Covers pageviews and attribution, the activation event, and browser-side or server-side conversions, then checks in OneLence that events arrive. Use when the user asks to add, install, set up, fix or verify OneLence tracking, or to track signups, purchases or other conversions with OneLence.
---

# Install OneLence tracking

Integrate OneLence into this project so the user can deploy and see visitors, attribution, activation and conversions in OneLence. Make the technical decisions yourself. Ask the user only plain-language questions you can't answer from the code, one at a time.

## 1. Get the site's setup from OneLence

1. Call `onelence_get_setup` with `response_format=detailed`. It returns:
   - the site, and whether events already arrive;
   - the defined conversion events;
   - the install instructions: the publishable key (`pk_…`), site id and host, npm and script snippets, the server-side conversion endpoint, and a step-by-step guide.

   Follow that guide; it is the source of truth for this workspace.
2. If the account has no site for this domain, offer to register it with `onelence_register_site`. That is a two-step confirmed write: show the summary and confirm only after the user agrees.
3. The publishable key is browser-safe. Never put a secret key (`sk_…`) or any server credential in browser code, public environment variables or source maps. OneLence tools never return secret keys. For server-side conversions the user creates a secret key in OneLence (Settings → API keys) and stores it only in the server environment as `ONELENCE_SECRET_KEY`; read it from there and never ask the user to paste it into the chat.

## 2. Inspect the project before changing anything

- Framework, rendering mode (SPA, SSR, static, hybrid), package manager and the app's client entry point.
- The signup or activation flow, and the main conversion: purchase, subscription, lead or booking.
- Whether a backend confirms conversions (payment webhooks, database writes).
- Existing analytics, and any consent or CMP setup.

## 3. Implement

- **Install and initialise once**
  - With a JavaScript build: install `@crelora/mark` with the project's package manager, then call `Mark.init({...})` once in the client root lifecycle, with the values from step 1 and `autocapture: { pageview: true }`.
  - Without a build: use the script snippet from step 1 in the global head or layout.
- **Base tracking**: let the SDK capture pageviews, visitor and session identity, and UTM and click-id attribution. Don't rebuild them by hand. Handle SPA route changes, double initialisation in development mode, and consent gating.
- **Activity**: `Mark.track('Event Name', {...})` for the real activation point and a few high-value actions. Don't create dozens of low-value events.
- **Conversions**: `Mark.conversion('Conversion Name', {...})` only for confirmed outcomes.
  - Prefer server-side or hybrid conversions when the backend confirms them, keeping the visitor attribution context the instructions describe.
  - Never send the same conversion from both browser and server unless the instructions say so.
- **Define the conversions in OneLence**: if a conversion isn't defined yet, add it with `onelence_save_event_definition` (two-step confirmed write) using the exact event name the code sends.
- **Consent**: respect the existing consent mechanism. Don't add a second one.
- **Existing analytics**: leave them as they are. OneLence runs alongside them.

## 4. Verify

1. Run the project's build, typecheck and tests.
2. After the user (or you, locally) visits the site and triggers the flows, call:
   - `onelence_verify_tracking` with a short `minutes` window, optionally passing an `event_name`;
   - `onelence_list_events` to see the event names and page paths that arrived.
3. If nothing arrives, check the init values, consent gating, ad blockers in the test browser and the site host, then verify again.

## 5. Report to the user, in non-technical language

- What OneLence now captures, which activation and conversions are tracked, and whether each conversion is browser-side, server-side or hybrid.
- What they still need to do: deploy, set the server environment variable, or check something in OneLence.
- How to verify it: exactly what to click on the site and what to expect in OneLence.

Docs: https://onelence.com/docs/integrations/start-integration/developer-setup and https://www.npmjs.com/package/@crelora/mark
