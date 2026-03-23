# PointSF Test Case (Claude)

## Pre-Test Requirement

Before starting the test, ensure that the device's compass and orientation sensors are functioning correctly. You can verify this by comparing compass readings with another reliable device or by checking through internal hardware diagnostics. Accurate compass calibration is essential for validating Scan View and POI alignment behaviors.

---

## App Launch Screen

1. **Launch the app for the first time**
   *Expected Outcome:* The PointSF logo splash screen displays for a few seconds, followed by a location permission request dialog.

2. **Deny location permission at launch**
   *Expected Outcome:* A message appears: "Location Permission Denied — To use this feature, please enable location access in your iPhone Settings." User cannot advance further.

3. **Allow location permission**
   *Expected Outcome:* The app proceeds to the POI loading screen.

4. **Set location permission to "Ask Next Time or When I Share"**
   *Expected Outcome:* The app requests location permission again upon launch.

5. **User outside San Francisco**
   *Expected Outcome:* Dialog displays: "This app is currently only available in San Francisco."

6. **Negative – Kill app before location prompt**
   *Expected Outcome:* App should not crash and should relaunch properly, re-prompting for location next time.

7. **Negative – GPS disabled at OS level**
   *Expected Outcome:* App shows a system or in-app prompt instructing the user to enable location services.

8. **Re-launch after permissions granted**
   *Expected Outcome:* On relaunch, splash and permission prompts do not reappear once permissions are granted.

9.  **`[NEW]` Launch app with location set to "While Using App", background it, then reopen**
    *Expected Outcome:* App correctly re-checks location on foreground and handles the permission state gracefully without crashing.

10. **`[NEW]` Negative – Revoke location permission via OS Settings and return to app**
    *Expected Outcome:* App detects the permission loss and shows the "Location Permission Denied" screen without crashing or freezing.

---

## POI Loading Screen

1. **Launch app after location permission is granted**
   *Expected Outcome:* POI loading screen appears with animated graphics representing loading POIs (not real data).

2. **Category filters visibility during loading**
   *Expected Outcome:* Category sorting filters remain hidden during loading.

3. **Verify POI caching behavior**
   *Expected Outcome:* POIs are prefetched and cached locally for faster reloads in Scan and Birds-eye views.

4. **Negative – API failure during POI load**
   *Expected Outcome:* App displays a retry message or default error popup without freezing.

5. **Negative – Cancel loading midway (force quit)**
   *Expected Outcome:* App gracefully resumes loading from the beginning next time.

6. **Slow network simulation**
   *Expected Outcome:* Loading animation continues smoothly; timeout or retry message appears under poor connectivity.

7. **`[NEW]` Return to app after POIs are cached — verify reload speed**
   *Expected Outcome:* Subsequent launches load POIs noticeably faster using the local cache compared to first load.

8. **`[NEW]` Verify loading screen animated icons are decorative only**
   *Expected Outcome:* POI marker icons shown during loading do not represent real database POI locations; they are purely animated graphics for effect.

9. **`[NEW]` Negative – Launch app in airplane mode (no network, no GPS)**
   *Expected Outcome:* App shows a meaningful error message — not a blank screen or crash.

---

## Scan View – Basics

1. **Default mode upon entering the app**
   *Expected Outcome:* App opens in Scan mode by default.

2. **Toggle between Scan and Birds-eye mode**
   *Expected Outcome:* User can switch between views using the toggle button. Smooth circular wipe animation plays.

3. **Category filter behavior**
   *Expected Outcome:* Only categories with visible POIs appear. Tapping toggles state. Horizontal scroll works smoothly.

4. **Parallax background layers**
   *Expected Outcome:* Three depth layers move at different speeds for realistic depth perception. Foreground moves with POIs.

5. **Distance band rotation**
   *Expected Outcome:* Distance arcs rotate smoothly as user pans left or right.

6. **POI marker scaling**
   *Expected Outcome:* POI markers change size based on distance (closer = larger). Three sizes should be visible across varying distances.

7. **Pointer alignment**
   *Expected Outcome:* Pointer remains upright and aligned during movement.

8. **Negative – Device compass calibration error**
   *Expected Outcome:* App detects calibration issue and prompts user to recalibrate.

9. **Recenter after background/resume**
   *Expected Outcome:* After minimizing and reopening the app, the pointer and compass recalibrate correctly.

10. **`[NEW]` Category filter – all categories deselected**
    *Expected Outcome:* All POI markers are displayed; UI remains stable and does not crash.

11. **`[NEW]` Category filter – deselect then re-select a category**
    *Expected Outcome:* POIs for that category reappear correctly without duplicates or rendering artifacts.

12. **`[NEW]` Verify zoom is disabled in Scan mode (V1 scope)**
    *Expected Outcome:* Pinch-to-zoom gesture in Scan mode has no effect; no zoom occurs.

---

## Scan View – Special Notes

1. **Dynamic POI range**
   *Expected Outcome:* Range adjusts automatically based on nearby POI density — tightens in dense areas, widens in sparse areas.

2. **No nearby POIs**
   *Expected Outcome:* Popup suggests switching to Birds-eye mode.

3. **Tap out-of-range POI**
   *Expected Outcome:* Dialog appears indicating POI is out of view.

4. **Tap-ability of POIs**
   *Expected Outcome:* Only POIs currently in focus can be tapped.

5. **180° blind zone**
   *Expected Outcome:* No POIs displayed behind the user.

6. **Negative – Rapid phone movement**
   *Expected Outcome:* UI performance remains smooth without flicker or lag.

7. **Negative – POI data latency**
   *Expected Outcome:* App continues showing cached POIs without freezing.

8. **`[NEW]` Walk from dense POI area to sparse area continuously**
   *Expected Outcome:* Dynamic range adjusts in real time without abrupt POI pop-in or sudden disappearance.

9.  **`[NEW]` User physically inside a POI location (Scan View)**
    *Expected Outcome:* Special marker or message appears on or near the pointer indicating the user is inside the POI. *(Note: exact behavior is TBD per spec — document observed behavior in current build.)*

---

## POIs in Focus

> **`[CAVEAT]`** The focused POI icon should grow larger **at its current screen location**, not jump to or appear at the center pointer. This is the new Scan View behavior. Birds-eye View may still show the old behavior (POI highlighted at center). Test and document both separately.

> **`[CAVEAT]`** Focus can change in two distinct ways: (1) via device heading / laser pointer movement, and (2) via scrolling the POI summary carousel cards. Both trigger mechanisms must be tested independently.

1. **`[REVISED]` Focus alignment feedback — visual**
   *Expected Outcome:* When pointer aligns with a POI, the marker grows larger with a glowing effect **at its current position on screen** (not at the center pointer).

2. **Focus alignment feedback — haptic**
   *Expected Outcome:* User receives a haptic tap when a POI comes into focus.

3. **Focus alignment feedback — audio**
   *Expected Outcome:* A sound plays on focus (optional — toggled via settings).

4. **Focus retention**
   *Expected Outcome:* Focus remains for 2–3 seconds or until another POI enters focus.

5. **`[REVISED]` Focus trigger via device heading (laser pointer)**
   *Expected Outcome:* As the user physically rotates the phone, the POI the pointer aligns with comes into focus.

6. **`[NEW]` Focus trigger via summary card scroll**
   *Expected Outcome:* Scrolling through overlapping POI summary cards changes which POI marker is focused/highlighted accordingly.

7. **`[NEW]` Scan View – focused POI grows at its location (not center)**
   *Expected Outcome:* In Scan View, the glowing enlarged state appears on the marker icon at its position in the view — not at the center pointer.

8. **`[CAVEAT]` Birds-eye View – focused POI behavior**
   *Expected Outcome:* In Birds-eye View, the focused POI may highlight at the center pointer (old behavior). Document the observed behavior and flag any discrepancy from the Scan View spec.

9. **Tap to lock focused POI**
   *Expected Outcome:* POI remains locked even as the phone moves.

10. **Display POI summary card**
    *Expected Outcome:* Card shows category, name, and distance. No close (x) icon.

11. **Get More Info**
    *Expected Outcome:* Opens POI detail view with AI-generated info.

12. **Negative – Multiple POIs enter focus quickly**
    *Expected Outcome:* Only one POI shows focus at a time. No overlap or flicker.

13. **Negative – Device vibration disabled**
    *Expected Outcome:* App does not crash; visual and audio feedback still appear.

14. **Focus handover rule**
    *Expected Outcome:* When two POIs overlap, the one nearest or most centered takes priority in focus.

15. **`[NEW]` Negative – Close (x) icon absent across all card states**
    *Expected Outcome:* No Close (x) icon appears on any POI summary card in any state — focused, locked, or in carousel.

---

## Locking / Unlocking a POI

> **`[CAVEAT]`** The team is experimenting with locking/unlocking via the **summary card** instead of the POI icon. Test both interaction methods and document which is active in the current build.

1. **Tap to lock POI (via POI icon)**
   *Expected Outcome:* Lock icon updates; POI remains fixed in focus even when phone moves.

2. **`[CAVEAT]` Lock via summary card interaction (experimental)**
   *Expected Outcome:* If locking via summary card is enabled in current build, tapping the card/lock area locks the POI. Document exact behavior observed.

3. **Flick gesture to unlock**
   *Expected Outcome:* Lock releases; user resumes scanning.

4. **`[NEW]` Tap POI icon to unlock (alternate unlock method)**
   *Expected Outcome:* Tapping the locked POI icon also releases the lock.

5. **`[CAVEAT]` Unlock via summary card (if card-based unlock is active)**
   *Expected Outcome:* Tapping the appropriate area of the summary card unlocks the POI. Document which unlock method is live in current build.

6. **First-time lock hint**
   *Expected Outcome:* "Flick to unlock" hint appears once per user and does not reappear on subsequent locks.

7. **Lock persistence**
   *Expected Outcome:* Locked POI remains locked after minimizing and reopening the app.

8. **`[NEW]` Lock icon visual state change**
   *Expected Outcome:* Lock icon visually differentiates between locked and unlocked states per mockup spec.

9. **`[NEW]` Attempt to scan while a POI is locked**
   *Expected Outcome:* Panning the phone does not change focus while the POI is locked.

10. **`[NEW]` Lock a POI, then switch from Scan to Birds-eye view**
    *Expected Outcome:* Locked state is either preserved or gracefully cleared on view switch — no crash or frozen state. Document observed behavior.

---

## Overlapping POIs

> **`[CAVEAT]`** The overlapping POI experience is currently known to be glitchy. For each test case below, use custom coordinates to reproduce the scenario and attach screenshots with steps-to-reproduce for any failure observed.

1. **Multiple POIs at same coordinates**
   *Expected Outcome:* Badge displays total number of overlapping POIs.

2. **Swipe through overlapping POIs**
   *Expected Outcome:* Vertical carousel scrolls through summary cards. As each card changes, the corresponding POI marker comes to the front.

3. **Closest POI order**
   *Expected Outcome:* Nearest POI displays first in the carousel.

4. **`[CAVEAT]` Carousel card / marker sync during swipe**
   *Expected Outcome:* Active summary card and its corresponding POI marker remain in sync. *(Known glitchy — document any desync with screenshot and custom coordinates.)*

5. **Negative – Rapid swipe through POIs**
   *Expected Outcome:* Cards and markers remain synced; no lag. *(Known glitchy — document failure cases.)*

6. **Negative – Close icon validation**
   *Expected Outcome:* No close (x) icon on summary cards.

7. **`[REVISED]` Carousel UI consistent between locked and unlocked states**
   *Expected Outcome:* Per spec note, the carousel UI shown in locked state should also apply in unlocked state. Verify consistency between both states.

8. **`[NEW]` Two POIs at exact same GPS coordinate — badge count = 2**
   *Expected Outcome:* Badge shows "2"; both POIs are accessible via swipe. Use custom coordinates to reproduce reliably.

9. **`[NEW]` Negative – Five or more POIs at same location (stress test)**
   *Expected Outcome:* All POIs accessible via carousel; badge count is accurate; no UI overflow or crash. Capture with screenshot.

10. **`[NEW]` Swipe carousel past the last card**
    *Expected Outcome:* Carousel stops at the last card or wraps — document observed behavior. No crash.

11. **`[NEW]` Overlapping POIs with a category filter active**
    *Expected Outcome:* Only POIs matching the active filter appear in the carousel; badge count updates accordingly.

---

## Birds-eye View

1. **Switch to Birds-eye mode**
   *Expected Outcome:* Smooth circular wipe transition animation plays.

2. **Pinch-to-zoom test**
   *Expected Outcome:* Map zooms in/out smoothly.

3. **Tap to focus POI**
   *Expected Outcome:* POI summary card appears and locks.

4. **Map pitch angle validation**
   *Expected Outcome:* Pitch matches 3D design spec. *(Note: pitch may be adjusted from mockup — document the current value.)*

5. **Negative – Internet disconnected**
   *Expected Outcome:* Cached POIs remain visible; show offline notice.

6. **Negative – Gesture conflict (zoom + rotate)**
   *Expected Outcome:* App handles combined gestures gracefully without crash.

7. **`[NEW]` Distance arcs present in Birds-eye view**
   *Expected Outcome:* Distance arc bands are visible in Birds-eye view, consistent with the Scan View display.

8. **`[NEW]` Scanning gesture (laser pointer) in Birds-eye view**
   *Expected Outcome:* User can use the scanning gesture to find and lock onto a specific POI in Birds-eye mode.

9. **`[NEW]` Switch back from Birds-eye to Scan mode**
   *Expected Outcome:* Circular wipe animation plays; Scan mode resumes correctly with pointer and compass intact.

10. **`[NEW]` POI outside current map viewport in Birds-eye view**
    *Expected Outcome:* Panning the map reveals POIs outside the initial view; no blank tile rendering or missing markers.

---

## POI Info Details Screen

1. **Open POI detail via "Get More Info"**
   *Expected Outcome:* Scrollable text displays AI-generated POI info.

2. **Multiple prompt pill buttons**
   *Expected Outcome:* Each pill highlights on tap and loads relevant response.

3. **`[NEW]` Tap each prompt pill in sequence**
   *Expected Outcome:* Each pill highlights correctly; its AI response loads in the text box without residual content from the previous prompt.

4. **Close details view**
   *Expected Outcome:* Returns to previous mode (Scan or Birds-eye).

5. **Negative – API timeout or AI error**
   *Expected Outcome:* Retry or "Unable to load info" message appears without freezing.

6. **Negative – Long AI response**
   *Expected Outcome:* Text scrolls smoothly; UI remains responsive.

7. **`[NEW]` AI response contains a URL link — tap the link**
   *Expected Outcome:* Link opens correctly in the default browser or in-app browser.

8. **`[NEW]` Return from detail screen — verify correct previous mode restored**
   *Expected Outcome:* Closing the detail screen returns to whichever mode the user was in (Scan or Birds-eye), not always Scan by default.

9. **`[NEW]` AI response in dark mode**
   *Expected Outcome:* Text, background, and pill buttons all render with correct dark mode theming.

---

## App Message Dialog Box

1. **Display standard app message**
   *Expected Outcome:* Centered popup with dimmed background appears.

2. **Contextual message placement**
   *Expected Outcome:* Message appears near related element with pointer arrow.

3. **Negative – Multiple dialogs triggered simultaneously**
   *Expected Outcome:* Only one dialog visible; others queued or dismissed.

4. **`[NEW]` Dismiss dialog via "Close" button**
   *Expected Outcome:* Dialog dismisses; background unblurs; user can interact with the app again.

5. **`[NEW]` Dismiss dialog via "Switch View" action button**
   *Expected Outcome:* Dialog dismisses and app switches to Birds-eye view correctly.

6. **`[NEW]` Dialog appears when tapping out-of-range POI**
   *Expected Outcome:* Dialog correctly states the POI is out of view or range.

---

## Dark Mode

1. **Enable system dark mode**
   *Expected Outcome:* UI switches correctly with proper contrast and visibility.

2. **Toggle dark ↔ light mode**
   *Expected Outcome:* Smooth transition; all screens adapt instantly.

3. **Negative – Incomplete theme switch**
   *Expected Outcome:* No missing icons or unreadable text.

4. **Negative – Sudden theme change during interaction**
   *Expected Outcome:* No flicker or layout misalignment.

5. **Dynamic elements theme validation**
   *Expected Outcome:* Dynamic content (AI-generated text, buttons, dialogs) properly switch themes in both modes.

6. **`[NEW]` POI marker icons in dark mode**
   *Expected Outcome:* POI marker colors and glowing focus effect are visible and distinguishable against the dark background.

7. **`[NEW]` Dark mode – loading screen**
   *Expected Outcome:* Animated loading icons render correctly against the dark background with no white flash.

8. **`[NEW]` Dark mode – Birds-eye map tiles**
   *Expected Outcome:* Map tiles switch to dark-variant tiles (if supported); no white flash on tile load.

---

## Transition Between Views

1. **Verify animation between Scan and Birds-eye mode**
   *Expected Outcome:* Smooth circular wipe animation plays every time without lag or frame drop.

2. **`[NEW]` Verify animation from Birds-eye back to Scan mode**
   *Expected Outcome:* Smooth circular wipe plays; Scan mode resumes correctly.

3. **`[NEW]` Negative – Rapid repeated toggling between views**
   *Expected Outcome:* No animation stacking, no UI freeze, no crash.

4. **`[NEW]` Toggle view while a POI is in focus**
   *Expected Outcome:* Focus state is handled gracefully on view switch — no dangling summary card or frozen state.

5. **`[NEW]` Toggle view while a POI is locked**
   *Expected Outcome:* Locked state is cleared or preserved consistently — document observed behavior. No crash.

---

## Inside POI Behavior

> *(Note: Final UX for "inside POI" behavior is TBD per spec. Test current build behavior and document observed outcome.)*

1. **User physically inside a POI**
   *Expected Outcome:* Special marker or message appears on pointer indicating user is inside the POI.

2. **`[NEW]` User enters then exits a POI boundary**
   *Expected Outcome:* Inside-POI state clears and normal POI marker state resumes on exit.

3. **`[NEW]` Multiple POIs at same location — user physically inside one**
   *Expected Outcome:* The correct POI is identified as "inside"; others display normally.

---

## Optional Extended QA Scenarios

1. **Performance benchmark**
   *Expected Outcome:* All transitions and animations run consistently at 60fps.

2. **Battery drain test**
   *Expected Outcome:* Continuous scanning for 10 minutes does not cause abnormal heating or battery drop.

3. **Orientation change test**
   *Expected Outcome:* Switching between portrait and landscape maintains layout integrity.

4. **Accessibility test**
   *Expected Outcome:* All text readable; voice-over identifies POIs; gestures compatible with accessibility mode.

5. **`[NEW]` Memory leak test – extended use (30+ min)**
   *Expected Outcome:* App memory usage stays stable over an extended session; no degradation in performance or unexpected crashes.

6. **`[NEW]` Cold start vs. warm start load time benchmark**
   *Expected Outcome:* Document cold start (fresh install) and warm start (cached POIs) load times in milliseconds for baseline comparison.

7. **`[NEW]` Background app refresh behavior**
   *Expected Outcome:* POI cache refreshes correctly on background refresh without requiring a full reload on next open.