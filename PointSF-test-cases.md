# PointSF Test Cases 

## Pre-Test Requirement

Before starting the test, ensure that the device's compass and orientation sensors are functioning correctly. You can verify this by comparing compass readings with another reliable device or by checking internal hardware diagnostics. Accurate compass calibration is essential for validating Scan View and POI alignment behavior.


## App Launch Screen

1. **Launch the app for the first time**  
   *Expected Outcome:* The PointSF logo splash screen displays for a few seconds, followed by a location permission request dialog.

2. **Grant location permission by selecting "Allow While Using App"/"While Using the App"**  
   *Expected Outcome:* The app proceeds to the POI loading screen.

3. **Launch the app with location set to "Allow While Using App"/"While Using the App", then background it, and reopen it**  
   *Expected Outcome:* The app correctly rechecks location on returning to the foreground and handles the permission state gracefully without displaying the permission prompt.

4. **Launch the app with location set to "Allow While Using App"/"While Using the App", then clear it from the background, and reopen it**  
    *Expected Outcome:* The app correctly rechecks location on returning to the foreground and handles the permission state gracefully without displaying the permission prompt.

5. **Set location permission to "Ask Next Time or When I Share"/"Allow Once"**  
   *Expected Outcome:* The app requests location permission again upon launch (the user needs to close and relaunch the app for the permission prompt to appear).

6. **Set location permission to "Never"/"Don't Allow"**  
   *Expected Outcome:* A message appears: "Location Permission Denied To use this feature, please enable location access in your iPhone Settings." User cannot advance further.

7. **GPS disabled at OS level (iOS Settings>Disable Location Services)**  
   *Expected Outcome:* App shows a system or in-app prompt instructing the user to enable location services.

8. **App version validation**   
    *Expected Outcome:* App launches successfully; version and build number match expected release details.

9. **User outside San Francisco**   
   *Expected Outcome:* Dialog displays: "This app is currently only available in San Francisco."

## POI Loading Screen

1. **Launch app after location permission is granted**  
   *Expected Outcome:* POI loading screen appears with animated graphics representing loading POIs (not real data) in both Scan and Birds-eye views.

2. **Category filters visibility during loading**  
   *Expected Outcome:* Category sorting filters remain hidden during loading in both Scan and Birds-eye views.

3. **Verify POI caching behavior**   
   *Expected Outcome:* POIs should load faster on subsequent launches or when returning to the app from background, resulting in reduced loading time and a smoother experience across Scan and Birds-eye views. The app should handle relaunch scenarios gracefully without blank screens.

4. **Force quit during loading and relaunch**  
   *Expected Outcome:* Loading restarts cleanly without corrupted state.

5. ***API failure during POI load**    
   *Expected Outcome:* A clear error or retry message is displayed when POIs fail to load, and the app remains responsive without freezing.

6. **Slow network simulation**     
   *Expected Outcome:* Loading animation continues smoothly; no UI freeze.


## Scan View 

1. **Enter app after loading completes**  
   *Expected Outcome:* The app opens in Scan mode by default and displays POIs along with category filters.

2. **Toggle between Scan and Birds-eye mode**   
   *Expected Outcome:* Users are able to switch between Scan and Birds-eye mode smoothly.

3. **Rapidly toggle between modes multiple times**    
   *Expected Outcome:* No crash, no UI corruption, animation remains stable.

4. **Move the device left to right and right to left**  
   *Expected Outcome:* The device heading updates accordingly.

5. **Verify pointer behavior**  
   *Expected Outcome:* The pointer remains fixed at the center and maintains an upright orientation at all times.

6. **Verify parallax background effect**   
   *Expected Outcome:* Background layers move at different speeds creating depth effect.

7. **Verify distance band rotation**   
   *Expected Outcome:* Distance arcs rotate smoothly with device movement, accurately display directional indicators (N, NE, E, SE, S, SW, W, NW), and correctly return to N after a full 360° rotation.

8. **Category filter behavior**   
   *Expected Outcome:* Selecting a category from the horizontal scroll filters the POIs to that category only and hides other categories. Deselecting the category shows all POIs again.

9. **POI marker scaling**   
   *Expected Outcome:* POI markers change size based on distance (closer = larger, farther = smaller).

10. **Minimize and resume app**   
   *Expected Outcome:* After minimizing and reopening the app, the pointer and compass recalibrate correctly.

11. **Dynamic POI range**   
   *Expected Outcome:* Range adjusts automatically based on nearby POI density — tightens in dense areas, widens in sparse areas. Walk from dense POI area to sparse area continuously.

12. **No nearby POIs scenario**    
   *Expected Outcome:* When no POIs are found within the visible range, the app suggests switching to Birds-eye view through a popup, helping the user discover POIs outside the current scan range.

13. **180° blind zone**   
   *Expected Outcome:* No POIs displayed behind the user. 

14. **User physically inside a POI location (Scan View)**   
    *Expected Outcome:* Special marker or message appears on or near the pointer indicating the user is inside the POI. 

15. **User enters then exits a POI boundary**   
   *Expected Outcome:* Inside-POI state clears and normal POI marker state resumes on exit.

16. **Rapid device movement (fast scanning)**    
   *Expected Outcome:* UI remains smooth; no flickering or jitter.

17. **Simulate compass calibration error**     
   *Expected Outcome:* App detects calibration issue and prompts user to recalibrate.


## POIs in Focus and Locking / Unlocking

1. **Align the pointer with a POI**   
   *Expected Outcome:* The POI enlarges, triggers haptic feedback and optional sound, and stays at its current position on the screen (not at the center pointer).

2. **Move device while POI is in focus**  
   *Expected Outcome:* Focus remains stable without flickering.

3. **Display POI summary card on focus**   
   *Expected Outcome:* The card shows the category, name, street address, and distance. In addition, it includes a "Get more info" option and a lock/unlock button.

4. **Tap focused POI to lock/unlock**  
   *Expected Outcome:* The POI remains fixed in focus, and the heading cannot be updated.

5. **Tap "Get more info" to view POI details**    
   *Expected Outcome:* Tapping "Get more info" opens a detailed view of the POI, displaying additional information generated in response to a curated prompt.

6. **Close POI detail view using (x) button**  
   *Expected Outcome:* Tapping the close (x) button dismisses the detail view and returns the user to the previous screen (Scan or Birds-eye view).

7. **Display multiple POI summary cards for overlapping POIs**   
   *Expected Outcome:* When multiple POIs overlap, multiple summary cards are displayed along with a POI count indicator.

8. **Scroll through overlapping POI summary cards**   
   *Expected Outcome:* Users can scroll vertically through overlapping POI cards maintaing an order based on distance, and each card is displayed correctly without UI glitches. 

9. **Verify focused POI marker updates with card selection (Scan-view mode)**   
   *Expected Outcome:* As the user scrolls through summary cards, the corresponding POI marker is highlighted and enlarges at its current screen position. Marker and card remain synchronized; no lag or mismatch.

10. **Multiple POIs with a category filter active**   
    *Expected Outcome:* Only POIs matching the active filter appear in the carousel; badge count updates accordingly.

11. **Verify POI summary card content and actions**  
   *Expected Outcome:* Each summary card displays correct information and includes "Get more info" and lock/unlock options.

12. **Device vibration disabled**   
   *Expected Outcome:* The app does not crash and shows no visual lag.

13. **Rotate device after locking POI**  
   *Expected Outcome:* POI remains locked despite rotating right to left and left to right.

14. **Unlock POI using flick gesture**   
   *Expected Outcome:* Lock is released; scanning resumes.

15. **Switch to Birds-eye view and return while POI is locked**  
   *Expected Outcome:* POI remains locked across mode transitions.

16. **Lock POI and then change category filters**     
   *Expected Outcome:* Locked POI behavior remains consistent or resets gracefully.

17. **Lock persistence**     
   *Expected Outcome:* Locked POI remains locked after minimizing and reopening the app.

18. **First-time lock interaction**   
   *Expected Outcome:* Hint (“flick to unlock”) appears once.

## Birds-eye View

1. **Switch to Birds-eye mode**   
   *Expected Outcome:* Map loads with smooth transition. Pitch matches 3D design.

2. **Pinch to zoom in and out**   
   *Expected Outcome:* Zoom is smooth and responsive.

3. **Distance arcs present in Birds-eye view**  
   *Expected Outcome:* Distance arc bands are visible in Birds-eye view, consistent with the Scan View display.

4. **Verify arc band adjustment on zoom in Bird’s-eye view**  
   *Expected Outcome:* Distance arc bands dynamically adjust their scale and spacing based on the zoom level (narrower range when zoomed in, wider range when zoomed out) while maintaining accurate distance representation.

5. **Scanning gesture (laser pointer) in Birds-eye view**  
   *Expected Outcome:* User can use the scanning gesture to find and lock onto a specific POI in Birds-eye mode.

6. **Switch back from Birds-eye to Scan mode**  
   *Expected Outcome:* Scan mode resumes correctly with pointer and compass intact.

7. **Perform combined gestures (zoom + rotate)**   
   *Expected Outcome:* App handles gestures without breaking interaction.

8. **Disconnect internet while in map view**   
   *Expected Outcome:* Cached POIs remain visible; offline message shown.

9. **Map re-entry state**   
   *Expected Outcome:* Re-entering Birds-eye view restores previous zoom and pitch levels.

## POI Info Details Screen

1. **Multiple prompt pill buttons**   
   *Expected Outcome:* Each pill highlights on tap and loads relevant response.

2. **Tap each prompt pill in sequence**   
   *Expected Outcome:* Each pill highlights correctly; its AI response loads in the text box without residual content from the previous prompt.

3. **Simulate API timeout or failure**    
   *Expected Outcome:* Error message shown; app remains responsive.

4. **Load long AI response**    
   *Expected Outcome:* Content scrolls smoothly without UI lag.

5. **AI response contains a URL link — tap the link**    
   *Expected Outcome:* Link opens correctly in the default browser or in-app browser.

## Dark Mode Appearance

1. **Enable system dark mode**  
   *Expected Outcome:* The UI adapts to the device’s default appearance (iOS Settings > Display & Brightness > Dark) with proper contrast and readability.

2. **Toggle between dark and light mode**   
   *Expected Outcome:* Smooth transition without flicker.

3. **Check dynamic content in dark mode**   
   *Expected Outcome:* AI content, buttons, and dialogs remain readable.

4. **Change theme during active interaction**   
   *Expected Outcome:* No layout shift or UI break.

5. **Incomplete theme switch**  
   *Expected Outcome:* No missing icons or unreadable text.

6. **AI response in dark mode**  
   *Expected Outcome:* Text, background, and pill buttons all render with correct dark mode theming.
   

## Transition Between Views

1. **Switch between Scan and Birds-eye repeatedly**   
   *Expected Outcome:* Circular wipe animation plays smoothly without frame drops.

2. **Toggle view while a POI is in focus**   
   *Expected Outcome:* Focus state is handled gracefully on view switch — no dangling summary card or frozen state.

3. **Toggle view while a POI is locked**   
   *Expected Outcome:* Locked state is cleared or preserved consistently — document observed behavior. No crash.

4. **Rapid repeated toggling between views**   
   *Expected Outcome:* No animation stacking, no UI freeze, no crash.


## Real-World Scenarios

1. **Walk while scanning POIs**  
   *Expected Outcome:* POIs update smoothly without jitter.

2. **Use app in a moving vehicle**  
   *Expected Outcome:* UI remains stable; no erratic behavior.

## Optional Extended QA Scenarios

1. **High POI density stress test (50+ POIs)**  
   *Expected Outcome:* No lag; stable performance.

2. **Continuous usage for 10 minutes**  
   *Expected Outcome:* No overheating or excessive battery drain.

3. **Orientation change test**  
   *Expected Outcome:* Switching between portrait and landscape maintains layout integrity.

4. **Accessibility testing (voice-over, readability)**  
   *Expected Outcome:* UI remains usable with accessibility features.

5. **Background app refresh behavior**  
   *Expected Outcome:* POI cache refreshes correctly on background refresh without requiring a full reload on next open.
