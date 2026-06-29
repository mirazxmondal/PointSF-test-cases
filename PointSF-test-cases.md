# PointSF Test Cases

## Pre-Test Requirement

Before starting the test, ensure that the device's compass and orientation sensors are functioning correctly. You can verify this by comparing compass readings with another reliable device or by checking internal hardware diagnostics. Accurate compass calibration is essential for validating Scan View and POI alignment behavior.

## App Launch Screen

1. **Launch the app for the first time**

   - **Expected Outcome:** The PointSF logo splash screen displays for a few seconds, followed by a location permission request dialog.

2. **Grant location permission by selecting "Allow While Using App" (iOS) / "While using the app" (Android)**

   - **Expected Outcome:** The app proceeds to the POI loading screen.

3. **Launch the app with location set to "Allow While Using App" (iOS) / "While using the app" (Android), then background it and reopen it**

   - **Expected Outcome:** The app correctly rechecks location on returning to the foreground and handles the permission state gracefully without displaying the permission prompt.

4. **Launch the app with location set to "Allow While Using App" (iOS) / "While using the app" (Android), then clear it from the background and reopen it**

   - **Expected Outcome:** The app correctly rechecks location on launch and handles the permission state gracefully without displaying the permission prompt.

5. **Set location permission to "Ask Next Time or When I Share" (iOS) / "Allow Once" or "Only this time" (Android)**

   - **Expected Outcome:** The app requests location permission again on the next app launch (the user may need to close and relaunch the app for the permission prompt to appear).

6. **Set location permission to "Never" (iOS) / "Don't allow" (Android)**

   - **Expected Outcome:** The app displays a message instructing the user to enable location permission in the device settings. The user cannot proceed further until permission is granted.

7. **GPS disabled at the OS level (iOS Settings / Android Location Settings)**

   - **Expected Outcome:** The app displays a system or in-app prompt instructing the user to enable location services before continuing.

8. **App version validation**

   - **Expected Outcome:** The app launches successfully, and the version and build number match the expected release details.

9. **User outside San Francisco**

   - **Expected Outcome:** A dialog displays: _"This app is currently only available in San Francisco."_

10. **Change location permission while the app is running**

       - **Expected Outcome:** The app detects the updated permission state when returning from Settings and updates its behavior without requiring a reinstall or leaving the app in an inconsistent state.

### Android-Specific Permission Tests

1. **Select "Don't ask again" (if supported by the Android version)**

   - **Expected Outcome:** The app no longer displays the system permission dialog and instead directs the user to Android Settings to grant location permission.

2. **Grant location permission after previously selecting "Don't ask again"**

   - **Expected Outcome:** After enabling location permission from Android Settings and returning to the app, the app detects the updated permission state and proceeds without requiring a restart.

3. **Revoke location permission from Android Settings while the app is installed**

   - **Expected Outcome:** On the next app launch or when returning to the foreground, the app detects the revoked permission and prompts the user to grant location access again.

4. **Disable Location Services from Android Settings while location permission remains granted**
   - **Expected Outcome:** The app detects that device location services are disabled and prompts the user to enable Location Services before continuing.

## POI Loading Screen

1. **Launch app after location permission is granted**

   - **Expected Outcome:** POI loading screen appears with animated graphics representing loading POIs (not real data) in both Scan and Birds-eye views.

2. **Category filters visibility during loading**

   - **Expected Outcome:** Category sorting filters remain hidden during loading in both Scan and Birds-eye views.

3. **Verify POI fetching for current hex and neighboring hexes**

   - **Expected Outcome:** When the user is located near the boundary of a hex, POIs from the current hex and its immediate neighboring hexes should be visible, ensuring no gaps in POI coverage across Scan and Birds-eye views.

4. **Verify reuse of cached POIs for already fetched hexes**

   - **Expected Outcome:** When revisiting a previously explored area (same hex), POIs should load without noticeable delay or refetch, indicating that cached hex data is being reused.

5. **Verify POI fetching on hex change (location movement)**

   - **Expected Outcome:** When the user moves to a new hex, POIs for the new current hex and its neighboring hexes should be fetched while maintaining a smooth transition without abrupt UI reloads.

6. **Verify cache eviction for distant hexes (beyond allowed range)**

   - **Expected Outcome:** When the user moves significantly away from previously visited areas, POIs from distant hexes should no longer persist, ensuring that only nearby POIs are retained.

7. **Verify smooth relaunch and background resume with cached data**

   - **Expected Outcome:** Upon relaunching the app or returning from background without significant location change, POIs should appear quickly without blank screens, leveraging cached data where applicable.

8. **Force quit during loading and relaunch**

   - **Expected Outcome:** Loading restarts cleanly without corrupted state.

9. **API failure during POI load**

   - **Expected Outcome:** A clear error or retry message is displayed when POIs fail to load, and the app remains responsive without freezing.

10. **Slow network simulation**

       - **Expected Outcome:** Loading animation continues smoothly; no UI freeze.

## Scan View

1. **Enter app after loading completes**

   - **Expected Outcome:** The app opens in Scan mode by default and displays POIs along with category filters.

2. **Toggle between Scan and Birds-eye mode**

   - **Expected Outcome:** Users are able to switch between Scan and Birds-eye mode smoothly.

3. **Rapidly toggle between modes multiple times**

   - **Expected Outcome:** No crash, no UI corruption, animation remains stable.

4. **Move the device left to right and right to left**

   - **Expected Outcome:** The device heading updates accordingly.

5. **Verify pointer behavior**

   - **Expected Outcome:** The pointer remains fixed at the center and maintains an upright orientation at all times.

6. **Align pointer with a POI**

   - **Expected Outcome:** The POI enlarges, triggers haptic feedback and optional sound, and stays at its current position on the screen.

7. **Move device away from focused POI**

   - **Expected Outcome:** The POI loses focus approximately **1 second** after it is no longer in focus, and the summary card disappears without waiting for scanning motion to stop.

8. **Continue scanning across POIs**

   - **Expected Outcome:** Focus shifts dynamically between POIs as they align with the pointer.

9.  **Display POI summary card on focus**

       - **Expected Outcome:** The card shows the category, name, street address, and distance. In addition, it includes a "Get more info" option and a lock/unlock button.

10. **Display multiple POI summary cards for overlapping POIs**

    - **Expected Outcome:** Up to **three** overlapping POI summary cards are displayed at a time along with the POI count indicator.

11. **Scroll through overlapping POI summary cards**

       - **Expected Outcome:** Users can scroll vertically through overlapping POI cards maintaing an order based on distance, and each card is displayed correctly without UI glitches.

12. **Verify focused POI marker updates with card selection**

       - **Expected Outcome:** As the user scrolls through summary cards, the corresponding POI marker is highlighted and enlarges at its current screen position. Marker and card remain synchronized; no lag or mismatch.

13. **Verify POI summary card content and actions**

       - **Expected Outcome:** Each summary card displays correct information and includes "Get more info" and lock/unlock options.

14. **Tap POI icon directly**

       - **Expected Outcome:** No action is triggered. POIs cannot be tapped directly in Scan View.

15. **Verify parallax background effect**

       - **Expected Outcome:** Background layers move at different speeds creating depth effect.

16. **Verify distance band rotation**

       - **Expected Outcome:** Distance arcs rotate smoothly with device movement, accurately display directional indicators (N, NE, E, SE, S, SW, W, NW), and correctly return to N after a full 360° rotation.

17. **Verify POI visibility within the second distance arc**

    - **Expected Outcome:** The second distance arc is positioned near the horizon, and POI markers are not clipped or hidden by the arc.

18. **Category filter behavior**

       - **Expected Outcome:** Selecting a category from the horizontal scroll filters the carousel to display only POIs belonging to the selected category and hides POIs from other categories. Deselecting the category restores all POIs.

19. **Verify POI marker scaling by distance**

       - **Expected Outcome:** POI markers scale dynamically based on their distance from the user (closer = larger, farther = smaller). Scaling updates smoothly as the user moves, with no abrupt size changes or rendering issues.

20. **Verify Transit POI marker shape and size consistency**

       - **Expected Outcome:** Transit POIs appear as square markers and maintain the same size in both the default and focused states, without scaling or enlargement.

21. **Minimize and resume app**

       - **Expected Outcome:** After minimizing and reopening the app, the pointer and compass recalibrate correctly. (Minimize the app while the device is pointing in one direction, then move the device and reopen the app. It should point to the new direction.)

22. **Dynamic POI range**

       - **Expected Outcome:** Range adjusts automatically based on nearby POI density, tightens in dense areas, widens in sparse areas. Walk from dense POI area to sparse area continuously.

23. **Switch to Birds-eye tip**

    - **Expected Outcome:** (Lat: 37.7575858 Lng: -122.4542809 H3 Hex: 8a283082da2ffff POIs within 500ft: 2 POIs within 500–1000ft: 6). The tip is displayed only when **three or fewer POIs** are within the Scan View range and additional POIs exist beyond the Scan View range. The updated message, **Dismiss** button, and **Switch view** action are displayed correctly, and the modal blocks interaction with the background until dismissed.

24. **User physically inside a POI location (Scan View)**

    - **Expected Outcome:** Special marker or message appears on or near the pointer indicating the user is inside the POI.

25. **User enters then exits a POI boundary**

       - **Expected Outcome:** Inside-POI state clears and normal POI marker state resumes on exit.

26. **Rapid device movement (fast scanning)**

       - **Expected Outcome:** UI remains smooth; no flickering or jitter.

27. **Simulate compass calibration error**

       - **Expected Outcome:** App detects calibration issue and prompts user to recalibrate.

28. **Device vibration disabled**

       - **Expected Outcome:** The app does not crash and shows no visual lag.

29. **Rotate device after locking POI**

    - **Expected Outcome:** The POI locks successfully, a single haptic feedback is triggered, and the POI remains locked despite rotating right to left and left to right.

30. **Unlock POI using flick gesture**

    - **Expected Outcome:** The lock is released, a single haptic feedback is triggered, and scanning resumes.

31. **Switch to Birds-eye View and return while POI is locked**

    - **Expected Outcome:** The POI remains locked across mode transitions, and the UI stays consistent.

32. **Lock POI and then change category filters**

    - **Expected Outcome:** The lock is cleared gracefully and the UI updates correctly.

33. **Lock persistence**

    - **Expected Outcome:** The locked POI remains locked after minimizing and reopening the app.

34. **First-time lock interaction**

    - **Expected Outcome:** The **"Flick your phone to scan..."** hint does not appear on app launch. It is displayed only after the user closes the POI details while the POI remains locked.

35. **180° blind zone**

    - **Expected Outcome:** No POIs are displayed behind the user.

36. **Verify Non-Parking Meter default zoom**

    - **Expected Outcome:** Scan View opens at the default zoom level. Distance arcs display **100 ft** and **200 ft**, the maximum scan range is **250 ft**, and only Non-Parking Meter POIs within **250 ft** are visible.

37. **Verify Non-Parking Meter Zoom In (+)**

    - **Expected Outcome:** Tapping the **+** button changes the distance arcs to **50 ft** and **100 ft**, reduces the maximum scan range to **125 ft**, and only Non-Parking Meter POIs within **125 ft** are visible.

38. **Verify Non-Parking Meter Zoom Out (−)**

    - **Expected Outcome:** Tapping the **−** button changes the distance arcs to **200 ft** and **400 ft**, increases the maximum scan range to **500 ft**, and additional Non-Parking Meter POIs within **500 ft** become visible.

39. **Verify Parking Meter default zoom**

    - **Expected Outcome:** With the Parking Meter category active, distance arcs display **10 ft** and **40 ft**, the maximum scan range is **50 ft**, and only Parking Meter POIs within **50 ft** are visible.

40. **Verify Parking Meter Zoom In (+)**

    - **Expected Outcome:** Tapping the **+** button changes the distance arcs to **5 ft** and **20 ft**, reduces the maximum scan range to **25 ft**, and only Parking Meter POIs within **25 ft** are visible.

41. **Verify Parking Meter Zoom Out (−)**

    - **Expected Outcome:** Tapping the **−** button changes the distance arcs to **20 ft** and **80 ft**, increases the maximum scan range to **100 ft**, and additional Parking Meter POIs within **100 ft** become visible.

42. **Rapidly change zoom levels**

    - **Expected Outcome:** Repeatedly tapping the **+** and **−** buttons causes no crashes, UI corruption, animation glitches, or incorrect POI rendering.

43. **Verify zoom limits**

    - **Expected Outcome:** The app prevents zooming beyond the minimum and maximum supported zoom levels. Additional presses of the **+** or **−** buttons have no effect.

44. **Change zoom while a POI is focused**

    - **Expected Outcome:** The focused POI remains focused if it is still within the visible range. The highlighted marker and summary card remain synchronized.

45. **Change zoom while a POI is locked**

    - **Expected Outcome:** The locked POI remains locked after changing zoom levels. The marker, summary card, and lock state remain consistent.

46. **Verify category filters after zoom**

    - **Expected Outcome:** The active category filter remains applied after changing zoom levels. Only POIs matching the selected category are displayed.

47. **Verify overlapping POIs after zoom**

    - **Expected Outcome:** Overlapping POIs continue to display the correct summary card carousel and POI count. Cards remain ordered by distance and synchronized with the highlighted marker.

48. **Switch between Scan and Birds-eye View after changing zoom**

    - **Expected Outcome:** The selected zoom level is preserved according to the product requirements after switching between Scan and Birds-eye View, with no UI inconsistencies.

49. **Minimize and resume after changing zoom**

    - **Expected Outcome:** After minimizing and reopening the app, the zoom level is restored (or reset to the default, if intended), with correct distance arcs, scan range, and POI positions.

50. **Verify POI visibility across zoom levels**

    - **Expected Outcome:** As the user zooms in and out, POIs correctly enter and leave the visible scan range without duplicates, missing markers, clipping, or incorrect positioning.

51. **Verify POI header line length**

       - **Expected Outcome:** The header line extends up to the second distance arc.

## Birds-eye View

1. **Switch to Birds-eye mode**

   - **Expected Outcome:** Map loads with a smooth transition. Pitch matches the 3D design.

2. **Pinch to zoom in and out**

   - **Expected Outcome:** Zoom is smooth and responsive.

3. **Distance arcs present in Birds-eye view**

   - **Expected Outcome:** Distance arc bands are visible and consistent.

4. **Verify arc band adjustment on zoom in Birds-eye view**

   - **Expected Outcome:** Distance arc bands dynamically adjust their scale and spacing based on zoom level (narrower range when zoomed in, wider range when zoomed out) while maintaining accurate distance representation.

5. **Verify default Birds-eye range**

   - **Expected Outcome:** At the default Birds-eye zoom level, POIs are displayed up to **750 ft**. POIs beyond **750 ft** are not displayed.

6. **Verify maximum Birds-eye range**

   - **Expected Outcome:** After zooming out to the maximum Birds-eye zoom level, POIs are displayed up to **1500 ft**. POIs beyond **1500 ft** are not displayed.

7. **Verify default Scan range from Birds-eye View**

   - **Expected Outcome:** Only POIs within the 500 ft range are visible and scannable.

8. **POI aligns with pointer in Birds-eye view**

   - **Expected Outcome:** The POI enters focus state (not locked) and displays a summary card.

9. **Move device away from focused POI**

   - **Expected Outcome:** The POI loses focus approximately **1 second** after it is no longer in focus, and the summary card disappears without waiting for scanning motion to stop.

10. **Tap an unfocused POI icon**

       - **Expected Outcome:** The POI becomes focused and locked immediately. The summary card is displayed and the POI icon changes to the focused state.

11. **Tap POI when multiple POIs are visible**

       - **Expected Outcome:** The selected POI becomes focused and locked, while other POIs remain unaffected.

12. **Tap a different POI while one POI is already locked**


    - **Expected Outcome:** The newly tapped POI becomes focused and locked, and the previously locked POI is released.

13. **Tap an already focused POI to lock**

    - **Expected Outcome:** The POI immediately becomes focused and locked, a single haptic feedback is triggered, the summary card is displayed, and the map orientation locks to the POI.

14. **Unlock a locked POI**

    - **Expected Outcome:** The POI exits the locked state, a single haptic feedback is triggered, the map orientation returns to normal, and the focus behavior resets.

15. **Move device after locking POI**

    - **Expected Outcome:** The locked POI remains fixed in focus and does not lose alignment.

16. **Verify focused POI marker updates with card selection**

       - **Expected Outcome:** As the user scrolls through summary cards, the corresponding POI marker is highlighted and enlarges at its current screen position. Marker and card remain synchronized; no lag or mismatch.

17. **Verify Transit POI marker shape and size consistency**

       - **Expected Outcome:** Transit POIs appear as square markers and maintain the same size in both the default and focused states, without scaling or enlargement.

18. **Perform combined gestures (zoom + rotate)**

    - **Expected Outcome:** The app handles gestures smoothly without breaking interaction.

19. **Unlock POI using flick gesture**

    - **Expected Outcome:** Lock is released; scanning resumes.

20. **Rapidly tap multiple POIs**

    - **Expected Outcome:** The app updates focus and lock state correctly without UI glitches or inconsistent states.

21. **Disconnect internet while in map view**

    - **Expected Outcome:** Cached POIs remain visible and an offline message is displayed.

22. **Map re-entry state**

    - **Expected Outcome:** Re-entering Birds-eye view restores the previous zoom and pitch levels.

23. **Lock persistence after app lifecycle changes**

    - **Expected Outcome:** The locked POI remains locked after minimizing and reopening the app.

24. **Birds-eye view with no POIs available**

    - **Expected Outcome:** The map loads correctly without errors, and an appropriate empty or fallback state is shown.

25. **Tap overlapping or closely placed POIs**

    - **Expected Outcome:** The correct POI is selected and highlighted.

26. **Rapid device movement while focusing POI**

    - **Expected Outcome:** Focus behavior remains stable or resets gracefully without flickering or inconsistent UI states.

27. **Verify POI header line length**

       - **Expected Outcome:** The header line extends up to the second distance arc.
  
## POI Icon Mapping

**Note:** Execute these test cases using the **POI Icon Mapping** dataset. Validate each supported POI category and subcategory at the specified coordinates. Verify both the default and focused icon states.

1. **Verify icon mapping for all POI types**

   - **Expected Outcome:** Every supported POI category and subcategory displays the correct default icon and focused icon according to the POI Icon Mapping specification.

2. **Verify POI icon consistency between Scan View and Birds-eye View**

   - **Expected Outcome:** Each POI displays the same icon in both Scan View and Birds-eye View. Switching between views does not change the assigned icon.

3. **Verify focused POI icon state**

   - **Expected Outcome:** When a POI gains focus, it displays the correct focused icon while maintaining the expected icon mapping.

4. **Verify Transit and Parking Meter marker rendering**

   - **Expected Outcome:** Transit Stops and Parking Meter POIs are displayed using their designated square markers and maintain their expected appearance in both the default and focused states.

5. **Verify POI icon consistency between marker and summary card**

   - **Expected Outcome:** The icon displayed on the POI marker matches the icon shown in the corresponding summary card.

6. **Verify fallback icon mapping**

   - **Expected Outcome:** POIs without a dedicated icon display the generic fallback icon while remaining visually consistent and distinguishable.

7. **Verify POI icon persistence**
   - **Expected Outcome:** POI icons remain correct after changing category filters, switching between Scan View and Birds-eye View, minimizing and reopening the app, and changing zoom levels.

## POI Info Details Screen

1. **Tap "Get more info" to view POI details**

   - **Expected Outcome:** Tapping **"Get more info"** opens a detailed view of the POI, displaying additional information generated in response to a curated prompt.

2. **Multiple prompt pill buttons**

   - **Expected Outcome:** Each pill highlights on tap and loads the relevant response.

3. **Tap each prompt pill in sequence**

   - **Expected Outcome:** Each pill highlights correctly, and its AI response loads without residual content from the previous prompt.

4. **Close POI detail view using (×) button**

   - **Expected Outcome:** Tapping the close (×) button dismisses the detail view and returns the user to the previous screen (Scan View or Birds-eye View).

5. **Simulate API timeout or failure**

   - **Expected Outcome:** An appropriate error message is displayed, and the app remains responsive.

6. **Load long AI response**

   - **Expected Outcome:** Long AI-generated content scrolls smoothly without UI lag.

7. **AI response contains a URL link, tap the link**

   - **Expected Outcome:** The link opens correctly in the default browser or in-app browser.

8. **Tap "Get more info" for a Transit Stop POI**

   - **Expected Outcome:** Tapping **"Get more info"** opens the designated external webpage instead of the internal AI response view.

9. **Tap "Get more info" on multiple Transit Stops and switch between them**

   - **Expected Outcome:** Each Transit Stop opens its corresponding webpage. Switching between stops does not display previously opened data, and the displayed stop matches the selected Transit POI.

10. **Press back from external webpage (Android specific)**

    - **Expected Outcome:** The user is returned to the POI screen.

11. **Close external webpage using the browser close option**

    - **Expected Outcome:** Closing the webpage returns the user to the app seamlessly without UI issues.

12. **Compare POI detail behavior by POI type**

    - **Expected Outcome:** Transit Stops open their designated external webpage, Parking Meter POIs open the ParkMobile webpage in an in-app webview, and all other POIs open the internal AI-generated POI detail view.

13. **Tap "Get more info" for a Parking Meter POI**

    - **Expected Outcome:** Tapping **"Get more info"** opens the ParkMobile webpage in an in-app webview.

14. **Verify Parking Meter webpage loads correctly**

    - **Expected Outcome:** The ParkMobile webpage loads successfully, allowing the user to enter the parking meter ID and continue with the payment flow.

15. **Tap "Get more info" with no internet connection**

    - **Expected Outcome:** An appropriate error page or message is displayed, and the app remains stable.

16. **Minimize app while an external webpage is loading**
    - **Expected Outcome:** On returning to the app, the webpage continues loading or is restored correctly without crashes or UI issues.

## Settings

1. **Open the Settings screen**

   - **Expected Outcome:** The Settings screen opens successfully and displays all available settings: **Sound**, **Display Mode**, **Parking Meters**, and **Scan Range**.

2. **Toggle Sound ON/OFF**

   - **Expected Outcome:** Sound effects are enabled or disabled accordingly. The selected state is applied immediately.

3. **Select Display Mode: System**

   - **Expected Outcome:** The app follows the device's current appearance setting (Light or Dark).

4. **Select Display Mode: Light**

   - **Expected Outcome:** The app switches to Light Mode immediately and all UI elements render correctly.

5. **Select Display Mode: Dark**

   - **Expected Outcome:** The app switches to Dark Mode immediately and all UI elements render correctly with proper contrast and readability.

6. **Switch between all Display Mode options**

   - **Expected Outcome:** Switching between **System**, **Light**, and **Dark** is smooth without UI glitches, missing icons, or unreadable text.

7. **Enable Parking Meter mode**

   - **Expected Outcome:** Only Parking Meter POIs are displayed. All other POI categories are hidden in both Scan View and Birds-eye View.

8. **Disable Parking Meter mode**

   - **Expected Outcome:** All supported POI categories are displayed again in both Scan View and Birds-eye View.

9. **Verify Parking Meter mode reset after app relaunch**

   - **Expected Outcome:** After closing and reopening the app, the Parking Meter toggle resets to **OFF**, and regular POIs are displayed.

10. **Verify Parking Meter mode reset after backgrounding the app**

    - **Expected Outcome:** After sending the app to the background and returning to the foreground, the Parking Meter toggle resets to **OFF** in both Scan View and Birds-eye View.

11. **Enable Parking Meter mode where no Parking Meter POIs exist**

    - **Expected Outcome:** (Lat: 37.776032, Lng: -122.480907) When no Parking Meter POIs are available nearby, the **"We couldn't find any nearby POI's"** dialog is displayed.

12. **Relaunch the app after the "No nearby POIs" scenario**

    - **Expected Outcome:** After dismissing the dialog and reopening the app, the Parking Meter toggle resets to **OFF**, and nearby non-Parking Meter POIs are displayed correctly.

13. **Verify Scan Range display**

    - **Expected Outcome:** The current Scan Range is displayed correctly and updates when the scan range changes.

14. **Reset Scan Range**

    - **Expected Outcome:** Tapping **Reset** restores the Scan Range to the default configuration, and the updated range is reflected in both Settings and Scan View.

15. **Verify lock and unlock icon appearance**
    - **Expected Outcome:** Lock and unlock icons match the design specification in both Light and Dark modes, including the correct foreground and background colors.

16. **Verify Sound setting persistence**

       - **Expected Outcome:** The selected Sound setting is retained after minimizing, reopening, and relaunching the app.

17. **Verify Display Mode persistence**

       - **Expected Outcome:** The selected Display Mode (System, Light, or Dark) is retained after minimizing, reopening, and relaunching the app.

## Transition Between Views

1. **Switch between Scan and Birds-eye repeatedly**

   - **Expected Outcome:** Circular wipe animation plays smoothly without frame drops.

2. **Toggle view while a POI is in focus**

   - **Expected Outcome:** Focus state is handled gracefully on view switch, no dangling summary card or frozen state.

3. **Toggle view while a POI is locked**

   - **Expected Outcome:** Locked state is cleared or preserved consistently, document observed behavior. No crash.

4. **Rapid repeated toggling between views**
   - **Expected Outcome:** No animation stacking, no UI freeze, no crash.

## Real-World Scenarios

1. **Walk while scanning POIs**

   - **Expected Outcome:** POIs update smoothly without jitter.

2. **Use app in a moving vehicle**
   - **Expected Outcome:** UI remains stable; no erratic behavior.

## Optional Extended QA Scenarios

1. **High POI density stress test (50+ POIs)**

   - **Expected Outcome:** No lag; stable performance.

2. **Continuous usage for 10 minutes**

   - **Expected Outcome:** No overheating or excessive battery drain.

3. **Orientation change test**

   - **Expected Outcome:** Switching between portrait and landscape maintains layout integrity.

4. **Background app refresh behavior**
   - **Expected Outcome:** POI cache refreshes correctly on background refresh without requiring a full reload on next open.

## Internal Settings & Location Method

### Internal Settings

1. **Verify Internal Settings are hidden by default**

   - **Expected Outcome:** The Internal Settings option is not visible when the app is launched normally.

2. **Open Internal Settings using the hidden gesture**

   - **Expected Outcome:** Tapping **Scan** three times followed by **Birds-eye View** four times in quick succession opens the Internal Settings screen.

3. **Verify incorrect unlock sequence**

   - **Expected Outcome:** Internal Settings remain hidden when the unlock sequence is performed incorrectly or with delays between taps.

4. **Verify Internal Settings reset after app relaunch**

   - **Expected Outcome:** After clearing the app from the background and reopening it, the Internal Settings option is hidden again.

### Location Method

1. **Verify Location Method is hidden by default**

   - **Expected Outcome:** The **Location Method** option is not visible anywhere in the main user interface.

2. **Open Location Method using the PointSF logo**

   - **Expected Outcome:** Tapping the **PointSF** logo three times opens the **Choose a Location Method** dialog.

3. **Open Location Method using the hidden gesture**

   - **Expected Outcome:** Tapping **Birds-eye View** twice followed by **Scan View** twice opens the **Choose a Location Method** dialog.

4. **Verify Location Method dialog UI**

   - **Expected Outcome:** The dialog displays correctly with all available location methods, input fields, radio buttons, and action buttons matching the expected design.

5. **Select "Set user current location"**

   - **Expected Outcome:** Tapping **Submit** updates the app to use the device's current location.

6. **Select "Set Center Point"**

   - **Expected Outcome:** Tapping **Submit** updates the app to use the selected center point.

7. **Select "Custom Coordinates"**

   - **Expected Outcome:** Entering valid latitude and longitude values and tapping **Submit** updates the app location to the specified coordinates.

8. **Select "Set HexID"**

   - **Expected Outcome:** Entering a valid HexID and tapping **Submit** updates the app location using the specified HexID.

9. **Verify invalid location input**

   - **Expected Outcome:** Invalid latitude, longitude, or HexID values are rejected with a clear validation message, and the current location remains unchanged.

10. **Verify out-of-coverage behavior**

    - **Expected Outcome:** Users outside the supported San Francisco boundary are shown the out-of-coverage modal at app launch.

11. **Verify in-coverage behavior**

    - **Expected Outcome:** Users inside the supported San Francisco boundary are not shown the out-of-coverage modal.

12. **Verify no nearby POIs behavior within the supported area**
    - **Expected Outcome:** Users inside the supported San Francisco boundary with no nearby POIs are shown the **"We couldn't find any nearby POIs"** dialog instead of the out-of-coverage modal.
