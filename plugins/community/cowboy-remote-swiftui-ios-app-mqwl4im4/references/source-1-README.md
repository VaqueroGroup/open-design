# Cowboy Remote — SwiftUI iOS app

A standalone SwiftUI app that mirrors the ScarfGo iOS surface but with the
COWBOY frontier-tech dark visual system.

## Build

Open in Xcode:

```sh
open Package.swift
```

Or from CLI:

```sh
swift build -Xswiftc -sdk -Xswiftc `xcrun --sdk iphoneos --show-sdk-path` \
  -Xswiftc -target -Xswiftc arm64-apple-ios17.0
```

## Run on simulator

```sh
xcodebuild -scheme CowboyRemote \
  -destination 'generic/platform=iOS Simulator' \
  -derivedDataPath build build

xcrun simctl boot "iPhone 16 Pro" 2>/dev/null
xcrun simctl install booted build/Build/Products/Debug-iphonesimulator/CowboyRemote.app
xcrun simctl launch booted com.vaquero.cowboyremote
```

## Structure

```
swift-remote/
├── Package.swift                                       SwiftPM manifest, iOS 17+
├── README.md
└── Sources/
    └── CowboyRemote/
        └── CowboyRemoteApp.swift                       single-file SwiftUI app
```

## What's in the app

7 tabs · 3 modals · single Swift file (`CowboyRemoteApp.swift`):

- **Projects** — Hermes project cards with status pills, awaiting approval pulse.
- **Monitor** — system strip + Dashboard / Activity / Queue sub-tabs.
- **Chat** — project-scoped conversational thread with tool-call bubbles and inline sign-off.
- **Sessions** — searchable session browser.
- **Skills** — per-profile skill inventory (New + Installed).
- **Memory** — `USER.md` / `MEMORY.md` entries with chip filters.
- **Settings** — server, profile, diagnostics, cron, logs.

Modals: profile switcher · diagnostics with 10 probes · lock-screen approval.

## Verification

`swiftc -parse-as-library -sdk iphoneos -target arm64-apple-ios17.0 -typecheck`
on `CowboyRemoteApp.swift` exits 0 with zero errors and zero warnings. Full
emit produces an iOS dylib (~931KB).