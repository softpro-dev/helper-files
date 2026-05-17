# Install Flutter on Mac

## 1. Install Flutter
```bash
brew install --cask flutter
which flutter && flutter --version
```

## 2. Verify setup
```bash
flutter doctor
```

## 3. iOS Simulator (macOS — no extra install if Xcode present)
```bash
# Accept Xcode license (one-time, needs password)
sudo xcodebuild -license accept

# Boot iPhone 16 Pro simulator
xcrun simctl boot "iPhone 16 Pro"
open -a Simulator

# Check booted
xcrun simctl list devices | grep Booted
```

## 4. Run app

While running → press `r` = hot reload, `R` = hot restart, `q` = quit.

### Browser (Chrome)
```bash
flutter run -d chrome
flutter run -d chrome --dart-define-from-file=env.json

```

### Android — Real Device
```bash
# 1. Enable Developer Options on phone → USB Debugging ON
# 2. Plug USB cable
flutter devices              # confirm device appears
flutter run -d <device-id>   # use id from flutter devices
flutter run -d 0G02A20X4000157C --dart-define-from-file=env.json # complete example of top command ( 0G02A20X4000157C dynamic, got by flutter devices command)

```

### Android — Emulator (Android Studio)
```bash
# Open Android Studio → Device Manager → start emulator
flutter devices              # emulator appears
flutter run -d <emulator-id>
# or shortcut:
flutter emulators --launch <emulator-id>
flutter run
```

### iOS — Xcode Simulator
```bash
# Boot simulator
xcrun simctl boot "iPhone 16 Pro"
open -a Simulator

# Run
flutter run -d "iPhone 16 Pro"
# or just:
flutter run   # select simulator from list
```

**This machine — iPhone 16 Pro (booted):**
```bash
flutter run -d 631C6B0C-4FED-4C8B-99A5-B93A5A0C7872
```

### iOS — Real iPhone
```bash
# 1. Connect iPhone via USB
# 2. Trust computer on iPhone
# 3. Open Xcode once → sign in with Apple ID → set team in Runner target
flutter devices              # iPhone appears
flutter run -d <device-id>
```

### Check all connected devices
```bash
flutter devices
```

## Installed (this machine)
- Flutter 3.41.9 (stable)
- Xcode 26.3
- iOS Simulator: iPhone 16 Pro (Booted ✓)
