---
title: "Notification Cockpit — PRD v0.1"
version: 0.1
date: 2026-09-25
status: draft
author: "product + platform engineering (agent session)"
audience: "senior iOS engineer; public APIs only"
platform_floor: "iOS 26 (proposed; operator to confirm — see Open Questions)"
license_proposal: "Apache-2.0 (proposed; operator to confirm)"
evidence_note: >-
  Every platform claim is labeled A–D. A = primary Apple doc fetched this
  run; B = claim retrieved this run via search with an Apple URL cited by
  the search engine, raw page not read; C = reputable secondary source;
  D = UNVERIFIED (prior knowledge or unresolvable this run). Direct fetches
  of developer.apple.com were blocked in this environment, so THIS DRAFT
  CONTAINS NO A-CLASS CLAIMS. All B-class claims require one confirmation
  pass against live Apple docs before v0.2.
sources_appendix: "§14"
---

# Notification Cockpit — PRD v0.1

An open-source iPhone notification cockpit that gamifies triage: users
process incoming alerts through a documented, multi-axis gesture language on
a surface the app actually owns (in-app inbox + optional Notification
Content Extension + Live Activities + widgets). The system Notification
Center remains the system Notification Center.

---

## 1. Problem and user

**Problem.** Notification volume outruns the triage affordances iOS gives a
single app: users either mass-clear (losing signal) or drown (losing focus).
No third-party app can improve triage of *other* apps' notifications — that
capability does not exist in public API [B, §14.2] — so the opportunity is a
best-in-class triage surface for notifications the app itself owns, plus a
methodology (Focus filters, scheduled-summary discipline, interruption-level
hygiene) the user applies system-wide.

**Primary user (proposed, operator to confirm).** A single person managing
high alert load who wants deliberate, fast, auditable triage: shift workers,
on-call engineers, ADHD users who benefit from externalized triage rituals.

## 2. Facts from research (cited; class labels per frontmatter)

### 2.1 Disconfirmation: "vacant system gesture we can occupy from the lock screen"

**The vacancy does not exist at the system layer.** No public API or
entitlement was found for overriding lock-screen gestures, adding
velocity-sensitive system swipes, or binding double-tap on a system
notification banner [B (absence claim), §14.2, §14.9]. Notification APIs
control content and presentation, never system gesture handling.
**Consequence:** the gesture invention is relocated to the app-owned surface
(in-app inbox, and — within documented limits — the Notification Content
Extension). This PRD does exactly that.

### 2.2 System notification interaction surface (current shipping iOS)

- Current shipping iOS is **iOS 26** (year-based naming adopted 2025) [B].
  Liquid Glass is a visual redesign; no notification gesture changes were
  found documented [C — secondary sources only; verify].
- Documented system interactions: **tap** opens the app at a relevant
  screen; **press-and-hold (long press)** expands the notification and
  reveals content plus action buttons; **swipe** to clear/manage [B — HIG
  Notifications]. Exact current affordance names for stack expand,
  clear-all, and Options/Manage: **UNVERIFIED this run [D]** — carried as a
  constraint, not a requirement.
- **Double tap, swipe velocity, and swipe distance are NOT documented as
  public Notification Center API surface** [D — no evidence found; treated
  as nonexistent per the design contract]. They appear in this PRD only as
  in-app axes.
- No dedicated "Playfulness"/gamification HIG page exists [B].

### 2.3 UserNotifications framework

- `UNNotificationAction` / `UNTextInputNotificationAction` provide buttons
  and inline text input on the app's own notifications [B].
- `UNNotificationCategory` with `customDismissAction` tells the app when the
  user intentionally dismisses one of its notifications [B].
- Interruption levels: `passive`, `active`, `timeSensitive`, `critical`
  (`UNNotificationInterruptionLevel`) [B]. Critical requires the restricted
  entitlement `com.apple.developer.usernotifications.critical-alerts`,
  granted only via Apple approval [B].
- `relevanceScore` (0–1) orders the app's notifications within the
  **Scheduled Summary**; `scheduledDeliverySetting` reports whether summary
  delivery applies [B].
- `threadIdentifier` groups the app's own notifications; `summaryArgument`
  is deprecated (deprecation OS version UNVERIFIED [D]) [B].
- Sandbox boundary: `getDeliveredNotifications` /
  `removeDeliveredNotifications` operate **only on the calling app's own
  notifications**. No public API reads, enumerates, or clears another app's
  notifications [B]. This is the load-bearing constraint of the product.

### 2.4 Extensions

- **Notification Content Extension** (`UNNotificationContentExtension`):
  a view controller rendered inside the app's own expanded (long-pressed)
  notification; handles action responses; media play/pause supported [B].
  Direct touch interactivity inside the extension view: **UNVERIFIED /
  conflicting this run [D]** — prior knowledge says it is off by default and
  enabled via the `UNNotificationExtensionUserInteractionEnabled` Info.plist
  key, but this was not confirmed against a fetched Apple doc. Carried in
  Constraints (§10), not Requirements.
- **Notification Service Extension** (`UNNotificationServiceExtension`):
  mutates remote-notification content when the payload sets
  `mutable-content: 1` with an alert; runs for a "limited amount of time"
  (the popular "~30 s" figure is not Apple-documented [D]); on failure the
  original content is shown [B].

### 2.5 Focus, Live Activities, widgets, App Intents

- **Focus filters**: `SetFocusFilterIntent` (iOS 16+) lets the app adjust
  behavior/content when the user's Focus changes, with user-configurable
  parameters [B].
- **Live Activities / ActivityKit**: Dynamic Island tap opens the app;
  touch-and-hold shows the expanded presentation; `Button(intent:)` /
  `Toggle(intent:)` (iOS 17+) run App Intents without opening the app;
  active up to 8 h, lock-screen persistence up to 12 h total [B]. The
  frequent-updates opt-in key name is UNVERIFIED [D].
- **Interactive widgets** (iOS 17+): only `Button` and `Toggle` backed by
  App Intents; no gestures, no custom interactive views; controls inactive
  while the device is locked [B].

### 2.6 App Review Guidelines

- **4.5.4**: push must not be required for the app to function; no
  promotions without explicit opt-in and an opt-out [B].
- **3.1.1**: randomized-reward purchase mechanics (loot boxes) must disclose
  odds; **5.3** gates real-money gaming [B]. Verbatim 4.3 (Spam) text
  UNVERIFIED this run [D].

## 3. Thesis and product principle (Thesis — labelled)

**Thesis.** The durable value is not a gesture gimmick; it is a
*triage discipline engine*: a fast, learnable, multi-axis gesture language on
an app-owned inbox, reinforced by ethical progression mechanics and deep
integration with the axes Apple already exposes (actions, extensions, Focus,
Live Activities, widgets, relevance scores). Apple can clone any single
gesture in one release; it is unlikely to clone an opinionated open-source
triage methodology with a developer-facing intent pack.

**Principle.** *Own your surface, respect the system.* Innovation happens
where touch delivery is documented; everything on system surfaces uses only
documented affordances.

## 4. Information architecture

- **Inbox** — the app-owned triage surface. Every item the app is authorized
  to know about (its own delivered notifications via
  `getDeliveredNotifications`, plus items mirrored in by integrations the
  user connects, e.g. email/webhook/RSS sources the app itself notifies for).
- **Stacks** — thread-grouped piles (mirroring `threadIdentifier` semantics)
  the user triages as a unit.
- **Focus lanes** — inbox partitions bound to Focus filter parameters; the
  active Focus selects the default lane.
- **Archive** — append-only record of triaged items with the verb applied;
  powers undo and the gamification ledger.

## 5. Gesture matrix

Axis legend: **public** = documented on system surface; **in-app-only** =
delivered only inside our own views; **extension-only** = inside our
Notification Content Extension; **UNVERIFIED** = not confirmed this run.

| System default (iOS 26) | App-owned analogue (inbox) | Input axes | Singular action | Combined / chorded action | Preview vs commit | Undo |
|---|---|---|---|---|---|---|
| Tap banner → open app [B] | Tap row | tap (public / in-app) | Select / open item | — | Commit (open) | Back returns; no state change |
| Long press → expand + actions [B] | Long press row | long press (public / in-app) | Preview + action sheet | Duration fork: short hold = preview, continued hold = pin | Preview first; explicit commit | Sheet dismiss = no-op |
| Swipe leading (system: reveal/manage; exact affordances UNVERIFIED [D]) | Swipe leading, **slow** | swipe distance + velocity (in-app-only) | Partial reveal: secondary actions (snooze, move lane, mute-craft) | Distance fork: partial reveal vs full-commit past threshold | Partial = preview; past threshold = commit | Rubber-band back cancels |
| — (velocity fork not public API [D]) | Swipe leading, **flick** | swipe velocity (in-app-only) | Clear / complete | Velocity fork of the same gesture | Commit | 5 s undo toast + Archive |
| Swipe trailing (system: clear/manage [B]) | Swipe trailing | swipe distance (in-app-only) | Open **or** archive (user-selectable default) | Distance fork: partial = other option, full = default | Partial = preview | Undo toast + Archive |
| — (no system double tap on banners [D]) | **Double tap row — the loaded vacant verb** | double tap (in-app-only) | **Quick-complete** (proposed default; operator to confirm) | — | Commit | Undo toast + Archive |
| — | Two-finger swipe down on a stack | multi-touch (in-app-only) | Triage whole stack with the lane's default verb | — | Confirm sheet above N items | Batch undo |
| — | Edge swipe from trailing edge | edge swipe (in-app-only) | Switch Focus lane | — | Commit (navigation) | Reverse swipe |
| 3D Touch / haptic press | — not designed against — | UNVERIFIED on current device classes [D] | — | — | — | — |

**Chord rule (enforced):** a gesture may fork only by velocity or duration,
never by hidden modes; every fork is discoverable in under two seconds via
the partial-reveal preview state.

**Accessibility (requirement, not option):** every verb is exposed as a
VoiceOver custom action and via Switch Control; a plain button-based action
sheet (long press or the row's disclosure control) reaches every verb.
Gamification is never the only path to clear an item.

**System-surface note:** on the Notification Content Extension, interaction
is limited to notification action buttons and — if
`UNNotificationExtensionUserInteractionEnabled` is confirmed [D] — simple
tap targets. No swipe/velocity language is promised there.

## 6. Gamification spec (ethical)

**Events (on-device ledger):** `item_completed`, `stack_batched`,
`inbox_zero_window`, `summary_respected` (acted after scheduled summary
rather than interrupting), `focus_compliant_triage`, `mute_crafted`.

**Scores:**
- **Triage XP** — awarded for batching and inbox-zero windows, capped per
  day (anti-grind).
- **Streaks** — consecutive days ending with an inbox-zero window.
- **Badges** — "Summary Respecter", "Focus Keeper", "Mute Smith"
  (crafted N precise mute rules).

**Anti-patterns (forbidden by spec):** variable-ratio rewards for *opening*
alerts; loot boxes or randomized rewards (also an App Review 3.1.1 hazard
[B]); push-to-reengage the same item; leaderboards ranking notification
volume. Telemetry is on-device by default; cloud sync is opt-in only.

## 7. Platform boundary table

| Feature | Public API | Entitlement | App Store likely | Sideload / OSS only | Impossible without private API |
|---|---|---|---|---|---|
| Custom lock-screen gesture override | None found [B-absence] | None found | — | — | **Yes** |
| Velocity-sensitive system swipe | None found [D] | — | — | — | **Yes** |
| Double-tap on a system banner | None found [D] | — | — | — | **Yes** |
| Content extension custom UI | `UNNotificationContentExtension` [B] | None | Yes | — | — |
| Content extension direct touch | `UNNotificationExtensionUserInteractionEnabled` — UNVERIFIED [D] | None known | Pending verification | — | — |
| Service extension mutate (own remote notifs) | `UNNotificationServiceExtension` [B] | None (APNs + mutable-content) | Yes | — | — |
| Focus filter | `SetFocusFilterIntent` [B] | None | Yes | — | — |
| Live Activity as standing inbox chip | ActivityKit [B] | None | Yes, within 8 h/12 h lifetime + update budgets [B] | Persistent "forever chip" not supported either way | — |
| Notification grouping control (own notifs) | `threadIdentifier`, `relevanceScore` [B] | None | Yes | — | — |
| Clearing another app's notification from our UI | **None** [B] | None | — | Not achievable by sideloading either (API absent, not policy-gated) | **Yes** |
| Critical alerts | `UNAuthorizationOptions.criticalAlert` [B] | Restricted; Apple approval required [B] | Only with granted entitlement | Entitlement still required | — |
| In-app multi-axis gesture language | UIKit/SwiftUI gesture recognizers | None | Yes | — | — |

**Shippable on App Store:** the entire cockpit as scoped (in-app inbox,
extensions, Focus filter, Live Activities, widgets, ethical gamification),
subject to 4.5.4 hygiene. **OSS/sideload-only:** nothing gains capability by
sideloading; the boundary is API absence, not review policy. **Cannot ship
anywhere:** any triage of other apps' notifications or system-gesture
override.

## 8. MVP / v1 / v2

- **MVP:** inbox + archive; tap / long-press / leading-swipe
  (slow-vs-flick) / trailing-swipe verbs with undo; double-tap
  quick-complete (pending operator confirmation); VoiceOver custom actions;
  on-device ledger with streaks only; one integration source (the app's own
  scheduled/local notifications).
- **v1:** Focus lanes via `SetFocusFilterIntent`; stacks + two-finger batch
  triage; Notification Content Extension (buttons-first; touch UI only after
  [D] verification); scheduled-summary compliance loop (`relevanceScore`);
  interactive widget with Button/Toggle intents; full badge set.
- **v2:** Live Activity triage chip (session-scoped, honest about the 8 h
  limit); App Intents pack exposing triage verbs to Shortcuts and third
  parties; opt-in encrypted sync; iPad/Mac exploration.

## 9. Open-source licence, repo layout, extension targets

- **Licence:** Apache-2.0 proposed (patent grant valuable for an SDK
  surface); MIT acceptable. Operator to confirm (§12).
- **Repo layout:** `App/` (SwiftUI app), `Kernel/` (triage engine + ledger,
  platform-free Swift package), `Extensions/NotificationContent/`,
  `Extensions/NotificationService/`, `Extensions/Widgets/` (widgets + Live
  Activities), `Intents/` (App Intents pack), `docs/` (this PRD, gesture
  contract, review-risk notes).
- **Targets:** app + content extension + service extension + widget
  extension; all public API.

## 10. Risks

- **App Review:** gamified notification mechanics may draw 4.5.4/spam
  scrutiny; mitigation = no engagement-bait pushes, all progression tied to
  *reducing* interruptions. Loot-box-shaped mechanics are banned by spec.
- **Attention ethics:** the failure mode is rewarding notification volume;
  the ledger design (XP caps, completion-not-opening events) is the control.
- **Apple platform change:** any system gesture/summary redesign (e.g. a
  future Liquid Glass interaction pass) can invalidate the analogue mapping;
  the in-app gesture kernel is deliberately independent of system surfaces.
- **Constraint carried from research (UNVERIFIED items, per contract):**
  content-extension touch interactivity [D]; exact system affordance names
  [D]; service-extension time budget number [D]; frequent-updates key [D];
  current 3D/haptic press availability [D]. None of these is a Requirement.

## 11. Kill criteria

1. Content-extension touch verification fails **and** in-app inbox D7
   retention < 15 % in beta — the surface thesis is wrong.
2. App Review rejects the gamified triage loop twice on 4.5.4/spam grounds
   with no compliant redesign path.
3. Apple ships first-party multi-verb notification triage at the system
   layer covering ≥ 80 % of the gesture matrix.
4. Median triage time per item in usability tests is not measurably better
   than stock swipe-clear.

## 12. Open questions for the operator (max 8)

1. iOS floor: iOS 26 only, or iOS 17+ (interactive widgets/Live Activity
   buttons) — which floor?
2. Confirm the vacant verb binding: double-tap = quick-complete **inside the
   app inbox** (never claimed on system banners)?
3. Primary user: you, a public OSS audience, or the shift-work/ADHD niche?
4. Licence: MIT or Apache-2.0; pure OSS or OSS core + paid sync/TestFlight?
5. Distribution: App Store-safe subset first, or full OSS cockpit first?
6. Which first integration source should feed the inbox at MVP (local
   schedules only, or a webhook/email bridge you run)?
7. Is the B2B "notification load analytics" lens (below) in or out of v1
   scope?
8. Do we pursue the critical-alerts entitlement for any use case, or
   explicitly renounce it?

## 13. Monetisation lens (Thesis — ranked, no invented TAM)

1. **High-value, low-volume:** developer SDK / App Intents pack for
   multi-axis notification actions; B2B "notification load" analytics for
   support/ops teams (opt-in, aggregate, privacy-preserving).
2. **High-volume, contested:** consumer "notification RPG" on the App Store
   — review risk and attention-economy risk both concentrate here.
3. **Adjacent:** accessibility / ADHD / shift-work Focus companion;
   open-source credibility as distribution, paid TestFlight or hosted sync
   optional.

**Where money will not go:** system-gesture novelty — Apple can clone any
single gesture in one iOS release, and no moat exists at that layer.

## 14. Sources appendix (fetched-this-run status)

Direct fetches of developer.apple.com were blocked in this environment; the
URLs below were cited by the search channel this run (class B) and must be
re-fetched for v0.2:

1. HIG Notifications — developer.apple.com/design/human-interface-guidelines/notifications
2. UNUserNotificationCenter (delivered-notification sandbox) — developer.apple.com/documentation/usernotifications/unusernotificationcenter
3. UNTextInputNotificationAction — developer.apple.com/documentation/usernotifications/untextinputnotificationaction
4. UNNotificationContentExtension — developer.apple.com/documentation/usernotificationsui/unnotificationcontentextension
5. UNNotificationServiceExtension — developer.apple.com/documentation/usernotifications/unnotificationserviceextension
6. relevanceScore / UNNotificationSettings — developer.apple.com/documentation/usernotifications
7. SetFocusFilterIntent — developer.apple.com/documentation/appintents/setfocusfilterintent
8. ActivityKit Live Activities — developer.apple.com/documentation/activitykit/displaying-live-data-with-live-activities
9. WidgetKit interactivity — developer.apple.com/documentation/widgetkit/adding-interactivity-to-widgets-and-live-activities
10. App Review Guidelines (4.5.4, 3.1.1, 5.3) — developer.apple.com/app-store/review/guidelines
11. Critical alerts entitlement — developer.apple.com/documentation/bundleresources/entitlements/com.apple.developer.usernotifications.critical-alerts
12. iOS 26 naming/release — apple.com/newsroom (June/Sept 2025), en.wikipedia.org/wiki/IOS_26

---

# Five highest-uncertainty Apple claims still needing a primary-source fetch

1. **Content-extension direct touch:** whether
   `UNNotificationExtensionUserInteractionEnabled` exists as documented, its
   default-off behavior, and what interaction it actually enables on iOS 26.
2. **Exact current system notification affordances on iOS 26:** verbatim HIG
   wording for stack expand, clear-all, and the Options/Manage controls
   (needed for an honest System-default column in the gesture matrix).
3. **HIG Gestures page content:** documented gesture vocabulary and the
   guidance against redefining system gestures (cited from prior knowledge
   only).
4. **Live Activity update budgets and the frequent-updates opt-in key**
   (`NSSupportsLiveActivitiesFrequentUpdates` — name unconfirmed), plus any
   iOS 26 changes to the 8 h/12 h lifetime.
5. **App Review Guideline 4.3 (Spam) verbatim text** and any current
   guidance touching gamified engagement mechanics beyond 3.1.1 loot-box
   odds disclosure.
