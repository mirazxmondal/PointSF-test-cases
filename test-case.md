# PointSF Master Test Case List

---

## App Launch Screen

1. **Launch the app for the first time**  
   *Expected Outcome:* The PointSF logo splash screen displays for a few seconds, followed by a location permission request dialog.

2. **Deny location permission at launch**  
   *Expected Outcome:* A message appears stating the user cannot proceed without enabling location access. User cannot advance further.

3. **Allow location permission**  
   *Expected Outcome:* The app proceeds to the POI loading screen.

4. **Set location permission to “Ask Next Time or When I Share”**  
   *Expected Outcome:* The app requests location permission again upon launch.

5. **User outside San Francisco**  
   *Expected Outcome:* Dialog displays: “This app is currently only available in San Francisco.”

6. **Negative – Kill app before location prompt**  
   *Expected Outcome:* App should not crash and should relaunch properly next time.

7. **Negative – GPS disabled at OS level**  
   *Expected Outcome:* App shows a system or in-app prompt instructing the user to enable location services.

8. **App version validation**  
   *Expected Outcome:* App launches successfully; version and build number match expected release details.

9. **Re-launch after permissions granted**  
   *Expected Outcome:* On relaunch, splash and permission prompts do not reappear once permissions are granted.

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
   *Expected Outcome:* POI markers change size based on distance (closer = larger).

7. **Pointer alignment**  
   *Expected Outcome:* Pointer remains upright and aligned during movement.

8. **Negative – Device compass calibration error**  
   *Expected Outcome:* App detects calibration issue and prompts user to recalibrate.

9. **Recenter after background/resume**  
   *Expected Outcome:* After minimizing and reopening the app, the pointer and compass recalibrate correctly.

---

## Scan View – Special Notes

1. **Dynamic POI range**  
   *Expected Outcome:* Range adjusts automatically based on nearby POI density.

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

---

## POIs in Focus

1. **Focus alignment feedback**  
   *Expected Outcome:* When pointer aligns with a POI, it glows, enlarges, triggers haptic feedback, and optionally plays sound.

2. **Focus retention**  
   *Expected Outcome:* Focus remains for 2–3 seconds or until another POI enters focus.

3. **Tap to lock focused POI**  
   *Expected Outcome:* POI remains locked even as the phone moves.

4. **Display POI summary card**  
   *Expected Outcome:* Card shows category, name, and distance. No close (x) icon.

5. **Get More Info**  
   *Expected Outcome:* Opens POI detail view with AI-generated info.

6. **Negative – Multiple POIs enter focus quickly**  
   *Expected Outcome:* Only one POI shows focus at a time. No overlap or flicker.

7. **Negative – Device vibration disabled**  
   *Expected Outcome:* App does not crash; visual and audio feedback still appear.

8. **Focus handover rule**  
   *Expected Outcome:* When two POIs overlap, the one nearest or most centered takes priority in focus.

---

## Locking / Unlocking a POI

1. **Tap to lock POI**  
   *Expected Outcome:* Lock icon updates; POI remains fixed.

2. **Flick gesture to unlock**  
   *Expected Outcome:* Lock releases; user resumes scanning.

3. **First-time lock hint**  
   *Expected Outcome:* “Flick to unlock” hint appears once per user.

4. **Negative – Rapid flick gesture spam**  
   *Expected Outcome:* App ignores excess flicks and remains stable.

5. **Lock persistence**  
   *Expected Outcome:* Locked POI remains locked after minimizing and reopening the app.

---

## Overlapping POIs

1. **Multiple POIs at same coordinates**  
   *Expected Outcome:* Badge displays total number of overlapping POIs.

2. **Swipe through overlapping POIs**  
   *Expected Outcome:* Vertical carousel scrolls through summary cards.

3. **Closest POI order**  
   *Expected Outcome:* Nearest POI displays first.

4. **Negative – Rapid swipe through POIs**  
   *Expected Outcome:* Cards and markers remain synced; no lag.

5. **Negative – Close icon validation**  
   *Expected Outcome:* No close (x) icon on summary cards.

---

## Birds-eye View

1. **Switch to Birds-eye mode**  
   *Expected Outcome:* Smooth transition animation plays.

2. **Pinch-to-zoom test**  
   *Expected Outcome:* Map zooms in/out smoothly.

3. **Tap to focus POI**  
   *Expected Outcome:* POI summary appears and locks.

4. **Map pitch angle validation**  
   *Expected Outcome:* Pitch matches 3D design spec.

5. **Negative – Internet disconnected**  
   *Expected Outcome:* Cached POIs remain visible; show offline notice.

6. **Negative – Gesture conflict (zoom + rotate)**  
   *Expected Outcome:* App handles combined gestures gracefully.

7. **Map re-entry state**  
   *Expected Outcome:* Re-entering Birds-eye view restores previous zoom and pitch levels.

---

## POI Info Details Screen

1. **Open POI detail via “Get More Info”**  
   *Expected Outcome:* Scrollable text displays AI-generated POI info.

2. **Multiple prompt pill buttons**  
   *Expected Outcome:* Each pill highlights on tap and loads relevant response.

3. **Close details view**  
   *Expected Outcome:* Returns to previous mode (Scan or Birds-eye).

4. **Negative – API timeout or AI error**  
   *Expected Outcome:* Retry or “Unable to load info” message appears without freezing.

5. **Negative – Long AI response**  
   *Expected Outcome:* Text scrolls smoothly; UI remains responsive.

---

## App Message Dialog Box

1. **Display standard app message**  
   *Expected Outcome:* Centered popup with dimmed background appears.

2. **Contextual message placement**  
   *Expected Outcome:* Message appears near related element with pointer arrow.

3. **Negative – Multiple dialogs triggered simultaneously**  
   *Expected Outcome:* Only one dialog visible; others queued or dismissed.

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

---

## Transition Between Views

1. **Verify animation between Scan and Birds-eye mode**  
   *Expected Outcome:* Smooth circular wipe animation plays every time without lag or frame drop.

---

## Inside POI Behavior

1. **User physically inside a POI**  
   *Expected Outcome:* Special marker or message appears on pointer indicating user is inside the POI.

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
