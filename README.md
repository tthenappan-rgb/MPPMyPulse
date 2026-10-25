# MPP – My Pulse Android project

This is an Android Studio project wrapper for the supplied `Updated MPP.html`, using the supplied MPP logo as the launcher icon.

## Build the APK
1. Open this project in Android Studio on a computer (Windows/macOS/Linux).
2. Allow Gradle to sync and install any requested Android SDK components (compile SDK 35).
3. Choose **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
4. The debug APK is normally created at `app/build/outputs/apk/debug/app-debug.apk`.
5. Test it on your own phone before sharing. For a release APK, use **Build → Generate Signed Bundle / APK → APK** and keep the signing key safe. All staff installs need a consistent signing key for future updates.

## Important testing notes
- The HTML file is copied unchanged into `app/src/main/assets/index.html`.
- The page currently references `html2pdf.js` from a CDN, so PDF export requires an internet connection unless that library is bundled locally.
- Test PDF export, WhatsApp launch, copy-to-clipboard, and any browser-specific actions on the built APK. WebView behavior may differ from Chrome.
- This project is source code, not a precompiled APK. It needs an Android SDK/Gradle build to produce an installable APK.


## Android WebView compatibility updates
- WhatsApp `wa.me` links are routed to an external Android app/browser rather than trapped in WebView.
- Copy Msg uses Android's native clipboard bridge when running in the APK, with the original browser fallback retained.
- PDF export asks Android's document picker where to save the generated PDF. The filename remains `MPP - Staff Name - Month Year.pdf`.
- PDF generation still loads `html2pdf.js` from a CDN, so the first PDF generation requires an internet connection.
- These code changes are prepared but must be compiled and tested on a real Android device before distribution.

## Build APK using GitHub Actions (phone-friendly cloud build)

This project includes `.github/workflows/build-apk.yml` to build a debug APK in GitHub's cloud. No Play Store account is required.

1. On your phone, sign in to GitHub and create a new **private** repository (recommended because this is a staff tool).
2. Upload the contents of this project folder to the repository root. Ensure `app/`, `build.gradle`, `settings.gradle`, `gradle.properties`, and `.github/workflows/build-apk.yml` are at the repository root level (do not upload an extra enclosing folder).
3. Open the repository's **Actions** tab. Select **Build MPP APK** and tap **Run workflow** (or push/commit the files to the `main` branch).
4. Wait for the workflow to complete successfully.
5. Open the completed workflow run, find **Artifacts**, and download `MPP-My-Pulse-APK`. Extract it to get `app-debug.apk`.
6. Transfer the APK to your phone or staff members. Android may require enabling permission to install apps from the app used to open the APK. Only install APKs from a source you trust.

This workflow produces a **debug APK** for testing and direct sharing, not a Play Store release. A successful cloud build still does not prove that WhatsApp and PDF features work on every device; test those on a phone before distributing.
