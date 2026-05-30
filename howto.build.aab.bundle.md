
# Pre-check before building:
``` bash
flutter doctor        # verify no issues
flutter pub get       # in each app dir

```


# Build AAB (Android) - for App Store
``` bash
flutter build appbundle --release --dart-define-from-file=env.prod.json 
```
- Output: build/app/outputs/bundle/release/app-release.aab
- AAB = Play Store format. Google splits it per device arch — smaller download for users.




# Build IPA (IOS)

``` bash
flutter build ipa --release --dart-define-from-file=env.prod.json
```

``` bash
open build/ios/archive/Runner.xcarchive
```
 
## Then open Xcode Organizer to export:
- Then open Xcode Organizer to export:
- Window → Organizer → Distribute App
- - Output: build/ios/ipa/*.ipa

