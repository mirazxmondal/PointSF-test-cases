# PointSF Test Cases (ChatGPT)

---

## Pre-Test Requirement

Before starting the test, ensure that:

- Device compass, gyroscope, and orientation sensors are functioning correctly  
- Location services are enabled  
- Test in both:
  - High POI density area  
  - Low POI density area  
- Network conditions:
  - Good / Slow / Offline  

---

## App Launch Screen

1. **Launch the app for the first time**  
   *Expected Outcome:* Splash screen appears for a few seconds, followed by location permission request dialog. 

2. **Deny location permission at launch**  
   *Expected Outcome:* Blocking message appears; user cannot proceed further.

3. **Allow location permission**  
   *Expected Outcome:* App proceeds to POI loading screen.

4. **Set location permission to “Ask Next Time or When I Share”**  
   *Expected Outcome:* App requests permission again on next launch.

5. **User outside supported region (non-SF location)** [REVISED]  
   *Expected Outcome:* Dialog appears: “This app is currently only available in San Francisco.”

6. **Kill app before permission prompt appears**  
   *Expected Outcome:* App relaunches without crash and shows correct flow.

7. **GPS disabled at OS level**  
   *Expected Outcome:* System or in-app prompt asks user to enable location services.

8. **Re-launch after permissions granted**  
   *Expected Outcome:* Permission prompt does not reappear; app proceeds normally.

---

## POI Loading Screen

1. **Launch app after granting location permission**  
   *Expected Outcome:* POI loading screen appears with animated placeholder markers (not real POIs).

2. **Verify category filters are hidden during loading**  
   *Expected Outcome:* Category filters are not visible during loading.

3. **Verify POI caching behavior (relaunch app)** [REVISED]  
   *Expected Outcome:* POIs load faster on relaunch due to caching.

4. **API failure during POI load**  
   *Expected Outcome:* Error or retry message appears; app does not freeze.

5. **Force quit during loading and relaunch** [REVISED]  
   *Expected Outcome:* Loading restarts cleanly without corrupted state.

6. **Slow network simulation**  
   *Expected Outcome:* Loading animation continues smoothly; no UI freeze.

---

## Scan View – Basics

1. **Enter app after loading completes**  
   *Expected Outcome:* App opens in Scan mode by default.

2. **Toggle between Scan and Birds-eye mode**  
   *Expected Outcome:* Circular transition animation plays smoothly without glitch.

3. **Rapidly toggle between modes multiple times** [NEW]  
   *Expected Outcome:* No crash, no UI corruption, animation remains stable.

4. **Pan device left and right** [REVISED]  
   *Expected Outcome:* POIs rotate smoothly around pointer.

5. **Verify pointer behavior**  
   *Expected Outcome:* Pointer always remains upright and centered.

6. **Verify parallax background effect**  
   *Expected Outcome:* Background layers move at different speeds creating depth effect.

7. **Verify distance band rotation**  
   *Expected Outcome:* Distance arcs rotate smoothly with device movement.

8. **Simulate compass calibration error**  
   *Expected Outcome:* App prompts user to recalibrate compass.

9. **Minimize and resume app**  
   *Expected Outcome:* Compass and pointer recalibrate correctly.

---

## Scan View – Special Notes

1. **Move between dense and sparse POI areas** [NEW]  
   *Expected Outcome:* POI range adjusts dynamically without sudden jumps or flicker.

2. **No nearby POIs scenario**  
   *Expected Outcome:* Popup suggests switching to Birds-eye view.

3. **Attempt to interact with out-of-range POI** [REVISED]  
   *Expected Outcome:* Message indicates POI is out of view.

4. **Verify POIs are not tappable unless in focus**  
   *Expected Outcome:* Only focused POIs respond to interaction.

5. **Rotate device 180° away from POIs**  
   *Expected Outcome:* No POIs shown in blind zone behind user.

6. **Rapid device movement (fast scanning)** [REVISED]  
   *Expected Outcome:* UI remains smooth; no flickering or jitter.

7. **Simulate delayed POI data response**  
   *Expected Outcome:* Cached POIs continue to display without freezing.

---

## POIs in Focus

1. **Align pointer with a POI**  
   *Expected Outcome:* POI enlarges, glows, triggers haptic feedback and optional sound.

2. **Slightly move device while POI is in focus** [NEW]  
   *Expected Outcome:* Focus remains stable without flickering.

3. **Move pointer away after focus is triggered**  
   *Expected Outcome:* Focus persists briefly (~2–3 seconds) before clearing.

4. **Rapidly scan across multiple POIs** [REVISED]  
   *Expected Outcome:* Only one POI is focused at a time; no visual flicker.

5. **Two POIs aligned (one closer, one centered)** [NEW]  
   *Expected Outcome:* Only one POI takes focus consistently; no rapid switching.

6. **Display POI summary card on focus**  
   *Expected Outcome:* Card shows category, name, and distance; no close (x) icon.

7. **Disable vibration in device settings**  
   *Expected Outcome:* No crash; visual and audio feedback still function.

8. **Turn off sound in app settings (if available)** [NEW]  
   *Expected Outcome:* No sound plays; other feedback remains intact.

---

## Locking / Unlocking a POI

1. **Tap focused POI to lock**  
   *Expected Outcome:* POI remains fixed in focus; lock state visible.

2. **Rotate device after locking POI** [NEW]  
   *Expected Outcome:* POI remains locked despite movement.

3. **Unlock POI using flick gesture**  
   *Expected Outcome:* Lock is released; scanning resumes.

4. **Switch to Birds-eye view and return while POI is locked** [NEW]  
   *Expected Outcome:* POI remains locked across mode transitions.

5. **Lock POI and then change category filters** [NEW]  
   *Expected Outcome:* Locked POI behavior remains consistent or resets gracefully.

6. **First-time lock interaction**  
   *Expected Outcome:* Hint (“flick to unlock”) appears once.

---

## Overlapping POIs

1. **Multiple POIs at same or similar coordinates**  
   *Expected Outcome:* Badge shows number of overlapping POIs.

2. **Swipe through overlapping POIs**  
   *Expected Outcome:* Vertical carousel updates summary cards correctly.

3. **Rapidly swipe carousel multiple times** [REVISED]  
   *Expected Outcome:* Marker and card remain synchronized; no lag or mismatch.

4. **Overlapping POIs with equal distance** [NEW]  
   *Expected Outcome:* Ordering remains stable and predictable.

5. **Verify no close (x) icon on summary cards**  
   *Expected Outcome:* UI matches design spec.

6. **Overlapping POIs interaction instability** [CAVEAT]  
   *Expected Outcome:* UI may behave inconsistently (known glitch); observe flicker, incorrect ordering, or desync.

---

## Birds-eye View

1. **Switch to Birds-eye mode**  
   *Expected Outcome:* Map loads with smooth transition.

2. **Pinch to zoom in and out**  
   *Expected Outcome:* Zoom is smooth and responsive.

3. **Tap on POI in map view**  
   *Expected Outcome:* Summary card appears and POI locks.

4. **Perform combined gestures (zoom + rotate)**  
   *Expected Outcome:* App handles gestures without breaking interaction.

5. **Disconnect internet while in map view**  
   *Expected Outcome:* Cached POIs remain visible; offline message shown.

---

## POI Info Details Screen

1. **Tap “Get more info” on a POI**  
   *Expected Outcome:* Scrollable AI-generated content is displayed.

2. **Interact with multiple prompt buttons**  
   *Expected Outcome:* Selected prompt highlights and updates content.

3. **Close details view**  
   *Expected Outcome:* Returns to previous mode (Scan or Birds-eye).

4. **Simulate API timeout or failure**  
   *Expected Outcome:* Error message shown; app remains responsive.

5. **Load long AI response**  
   *Expected Outcome:* Content scrolls smoothly without UI lag.

---

## App Message Dialog Box

1. **Trigger standard dialog message**  
   *Expected Outcome:* Centered popup appears with dimmed background.

2. **Trigger contextual message (with pointer)**  
   *Expected Outcome:* Message appears near relevant UI element.

3. **Trigger multiple dialogs simultaneously**  
   *Expected Outcome:* Only one dialog visible at a time.

---

## Dark Mode

1. **Enable system dark mode**  
   *Expected Outcome:* UI switches with proper contrast and readability.

2. **Toggle between dark and light mode**  
   *Expected Outcome:* Smooth transition without flicker.

3. **Check dynamic content in dark mode**  
   *Expected Outcome:* AI content, buttons, and dialogs remain readable.

4. **Change theme during active interaction**  
   *Expected Outcome:* No layout shift or UI break.

---

## Transition Between Views

1. **Switch between Scan and Birds-eye repeatedly** [REVISED]  
   *Expected Outcome:* Circular wipe animation plays smoothly without frame drops.

---

## Inside POI Behavior

1. **User is physically inside a POI location**  
   *Expected Outcome:* Special indicator or message appears near pointer.

---

## Real-World Scenarios

1. **Walk while scanning POIs**  
   *Expected Outcome:* POIs update smoothly without jitter.

2. **Use app in a moving vehicle** [NEW]  
   *Expected Outcome:* UI remains stable; no erratic behavior.

3. **Use app indoors (weak GPS)** [NEW]  
   *Expected Outcome:* App degrades gracefully; no crashes.

---

## Optional Extended QA Scenarios

1. **High POI density stress test (50+ POIs)** [NEW]  
   *Expected Outcome:* No lag; stable performance.

2. **Continuous usage for 10 minutes**  
   *Expected Outcome:* No overheating or excessive battery drain.

3. **Orientation change (portrait ↔ landscape)**  
   *Expected Outcome:* Layout remains intact.

4. **Accessibility testing (voice-over, readability)**  
   *Expected Outcome:* UI remains usable with accessibility features.