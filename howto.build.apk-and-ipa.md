
# Pre-check before building:
``` bash
flutter doctor        # verify no issues
flutter pub get       # in each app dir

```


# Build APK (Android)
``` bash
flutter build apk --release --dart-define-from-file=env.prod.json 
```
- Output: build/app/outputs/flutter-apk/app-release.apk
- For Play Store → use flutter build appbundle instead (generates .aab)
 


# Build IPA (IOS)

``` bash
flutter build ipa --release --dart-define-from-file=env.prod.json
```
 
## Then open Xcode Organizer to export:
- Then open Xcode Organizer to export:
- Window → Organizer → Distribute App
- - Output: build/ios/ipa/*.ipa

