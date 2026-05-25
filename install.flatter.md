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


### Browser (Chrome)
```bash
flutter run -d chrome --dart-define-from-file=env.json

flutter run -d chrome --dart-define-from-file=./../env.json
```

### Android — Real Device
```bash
# 1. Enable Developer Options on phone → USB Debugging ON
# 2. Plug USB cable
flutter devices              # confirm device appears
flutter run -d <device-id>   # use id from flutter devices
flutter run -d 0G02A20X4000157C --dart-define-from-file=env.json 

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



### Android — Emulator (Android Studio)

**Create new emulator (one-time):**
1. Open Android Studio
2. `More Actions` → `Virtual Device Manager` (or `Tools` → `Device Manager`)
3. Click `+` → `Create Virtual Device`
4. Pick hardware profile (e.g. `Pixel 8`) → Next
5. Download a system image (e.g. `API 35 / Android 15`) → Next
6. Name it → Finish

**Launch & run:**
```bash
flutter emulators                       # list all created emulators
flutter emulators --launch <id>         # boot one (e.g. Pixel_8_API_35)
flutter devices                         # confirm emulator appears
flutter run -d <emulator-id>
# or after emulator is booted, just:
flutter run                             # Flutter auto-selects running emulator
```

**Command-line only (no Android Studio UI):**
```bash
# List available system images
sdkmanager --list | grep "system-images"

# Create AVD via avdmanager
avdmanager create avd \
  -n Pixel8_API35 \
  -k "system-images;android-35;google_apis;x86_64" \
  -d pixel_8

# Boot it
emulator -avd Pixel8_API35
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
 
## Installed (this machine)
- Flutter 3.41.9 (stable)
- Xcode 26.3
- iOS Simulator: iPhone 16 Pro (Booted ✓)
