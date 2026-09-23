# WallTunes

A 24/7 music player for a wall-mounted Fire TV. Add songs from your phone, and it plays them on repeat forever.

## Build the APK

**Option A: GitHub (no installs)**
1. Push this folder to a new private GitHub repo.
2. Open the repo's **Actions** tab. The "Build APK" job runs on every push.
3. When it finishes, open the run and download **WallTunes-apk** (a zip with `app-release.apk` inside).

**Option B: Android Studio**
Open this folder, wait for Gradle to sync, then run **Build > Build App Bundle(s) / APK(s) > Build APK(s)**.

The APK is signed with the key in `app/keys/`, so new builds install right over old ones and your songs stay put. Keep the repo private.

## Install it on the Fire TV

1. Fire TV: **Settings > My Fire TV (or Device & Software) > About**, then click the TV name 7 times.
2. In **Developer Options**, turn on **ADB debugging** and **Apps from unknown sources**.
3. Install:
   - **From your PC:** `adb connect <TV-IP>:5555`, accept the prompt on the TV, then `adb install -r app-release.apk`
   - **Or with Downloader:** upload the APK somewhere (like itsdalton.com), install the free *Downloader* app on the TV, type the link, and install.
4. Optional, lets the screen open itself after the TV restarts:
   `adb shell appops set com.itsdalton.walltunes SYSTEM_ALERT_WINDOW allow`

## Using it

- Open WallTunes. Scan the QR code with your phone (same Wi-Fi) to add songs, skip, shuffle, or delete.
- Remote: **Select** play/pause, **Left/Right** previous/next, **Up** shuffle, **Down** show/hide the QR code.
- **Back** closes the screen, but the music keeps playing. Reopen the app to see it again.

## Where things live

- `PlaybackService.kt`: the player, library, auto-resume.
- `UploadServer.kt`: the web server on port 8080.
- `MainActivity.kt`: the TV screen and remote controls.
- `assets/upload.html`: the phone page.
