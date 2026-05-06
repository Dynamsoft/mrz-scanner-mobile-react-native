# Dynamsoft MRZ Scanner — React Native Sample (ScanMRZ)

This repo hosts **ScanMRZ**, a complete React Native sample app demonstrating the Dynamsoft MRZ Scanner ready-to-use scanning UI. It scans the Machine Readable Zone (MRZ) on passports and ID cards and renders the parsed fields, captured document images, and portrait photo.

The sample is built around `MRZScanner` from [`dynamsoft-mrz-scanner-bundle-react-native`](https://www.npmjs.com/package/dynamsoft-mrz-scanner-bundle-react-native), which packages the camera UI, scanning logic, and result delivery into a single launch call.

## Features

- Scans the MRZ on passports and ID cards through the ready-to-use `MRZScanner` UI.
- Parses the MRZ into structured fields — name, date of birth, document number, expiry, nationality, and more.
- Returns the portrait image extracted from the document, plus processed and original captures of both the MRZ side and the opposite side.

The full scan flow lives in a single file: [ScanMRZ/src/App.tsx](ScanMRZ/src/App.tsx).

## Quick Start

```bash
# 1. Clone the repo
git clone https://github.com/Dynamsoft/mrz-scanner-mobile-react-native-dev.git
cd mrz-scanner-mobile-react-native-dev/ScanMRZ

# 2. Install JavaScript dependencies
npm install

# 3. Install iOS native dependencies
cd ios && bundle exec pod install --repo-update && cd ..
```

All remaining commands in the sections below run from the `ScanMRZ` directory.

> [!IMPORTANT]
> Both platforms must be run on a **physical device**. The iOS simulator and most Android emulators do not expose a working camera to the SDK.

## Configure Your License

A valid license key is required to use the SDK. The sample ships with a public trial license string in [ScanMRZ/src/App.tsx:62](ScanMRZ/src/App.tsx#L62):

```tsx
let mrzScanConfig = {
  license: 'DLS2eyJvcmdhbml6YXRpb25JRCI6IjIwMDAwMSJ9',
} as MRZScanConfig;
```

This trial string is time-limited and **requires a network connection**. To request your own 30-day trial, visit [Request a Trial License](https://www.dynamsoft.com/customer/license/trialLicense?product=mrz&utm_source=samples&package=react-native), then replace the `license` value in `App.tsx` with the key you receive.

## Run the Sample

### iOS

The iOS project must be signed before it will install on a device:

1. Open `ios/ScanMRZ.xcworkspace` in Xcode.
2. Select the project, open the **Signing & Capabilities** tab, and set a valid **Team**.

Connect a physical iOS device, then launch using either option below.

**Option A — Run from Xcode.** Select your connected device from the top bar and click **Run**.

**Option B — Run from the command line.** Pass the `--device` flag, otherwise React Native defaults to the simulator (which will not work for this sample):

```bash
npx react-native run-ios --device
```

If multiple devices are connected, target one explicitly:

```bash
npx react-native run-ios --device "DEVICE-NAME"
```

### Android

Connect a physical Android device with USB debugging enabled, then run:

```bash
npm run android
```

You can list connected devices with `adb devices`.

## Supported Document Types

The SDK supports the three ICAO Machine Readable Travel Document (MRTD) formats:

- **TD1** — ID cards with a 3-line MRZ.
- **TD2** — ID cards with a 2-line MRZ.
- **TD3** — passports with a 2-line MRZ.

For support for other MRTD types, contact the [Dynamsoft Support Team](https://www.dynamsoft.com/contact/).

## System Requirements

- React Native **0.71.0** or higher (this sample is pinned to **0.79.0**).
- Node **18** or higher.
- **Android**
  - Supported OS: Android 5.0 (API Level 21) or higher.
  - Supported ABIs: armeabi-v7a, arm64-v8a, x86, x86_64.
  - Development environment: Android Studio 2022.2.1+ (2025.2.1 recommended), Java 17+, Gradle 8.0+.
- **iOS**
  - Supported OS: iOS 13 or higher.
  - Supported ABIs: arm64, x86_64.
  - Development environment: Xcode 13+ (Xcode 14.1+ recommended).

## Project Structure

```
ScanMRZ/
├── src/
│   ├── App.tsx                          # Scan flow + result UI (entire app)
│   └── assets/
│       └── ic_portrait_placeholder.jpg  # Fallback when no portrait is captured
├── android/                             # Native Android project
├── ios/                                 # Native iOS project (Podfile, .xcworkspace)
├── index.js                             # Registers App as the root component
└── package.json                         # Pinned to dynamsoft-mrz-scanner-bundle-react-native@3.4.1300
```

## Platform Configuration

The sample is already configured for both platforms. The notes below explain what is wired up, in case you adapt the sample code into your own project.

- **iOS** — [ScanMRZ/ios/ScanMRZ/Info.plist](ScanMRZ/ios/ScanMRZ/Info.plist) declares `NSCameraUsageDescription`. Without this, the app would crash the moment the scanner tries to open the camera.

  ```xml
  <key>NSCameraUsageDescription</key>
  <string>This app uses the camera to scan MRZ documents.</string>
  ```

- **Android** — no manual permission changes are required. The SDK's manifest merges the `CAMERA` permission automatically. The trial license needs network access, so the default `INTERNET` permission in `android/app/src/main/AndroidManifest.xml` is left in place:

  ```xml
  <uses-permission android:name="android.permission.INTERNET" />
  ```

## Documentation

- **[User Guide](https://www.dynamsoft.com/mrz-scanner/docs/mobile/programming/react-native/user-guide/index.html)** — step-by-step walkthrough of building an MRZ scanning app with the React Native SDK from scratch.
- **[Customization Guide](https://www.dynamsoft.com/mrz-scanner/docs/mobile/programming/react-native/user-guide/customize-mrz-scanner.html)** — deeper customization of `MRZScanConfig`, including document-type filtering, UI button visibility, and image capture settings.
- **[API Reference](https://www.dynamsoft.com/mrz-scanner/docs/mobile/programming/react-native/api-reference/index.html)** — full type definitions for `MRZScanner`, `MRZScanConfig`, `MRZScanResult`, and `MRZData`.

## Support

For help, integration questions, or custom requirements, contact the [Dynamsoft Support Team](https://www.dynamsoft.com/contact/).

## License

See [LICENSE.md](LICENSE.md). The sample code in this repository is distributed under the terms of the [Dynamsoft Software License Agreement](https://www.dynamsoft.com/company/license-agreement/).
