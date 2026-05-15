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
```bash
# In app:rider directory
flutter run           # prompts to choose device
flutter run -d macos  # macOS desktop
flutter run -d chrome # Chrome browser
flutter run -d <simulator-udid>  # specific simulator
```

## Installed (this machine)
- Flutter 3.41.9 (stable)
- Xcode 26.3
- iOS Simulator: iPhone 16 Pro (Booted ✓)
