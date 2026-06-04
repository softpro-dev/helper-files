# Each app folder run
``` bash
flutter pub add flutter_launcher_icons --dev
```
# Then update /pubspec.yaml
```yaml
flutter_launcher_icons:
  android: true
  ios: true
  image_path: "assets/icon/app-icon-fleet-1024x1024.png"
```
# Then run
``` bash
dart run flutter_launcher_icons
```
