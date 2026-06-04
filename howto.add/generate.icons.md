# Generate Launcher Icons (app:all)

## Setup (one-time per app)

`flutter_launcher_icons: ^0.14.4` already added in dev_dependencies of all 3 apps.

## Icon files needed

| App | Path |
|-----|------|
| app-rider | `assets/icon/app-icon-1024x1024.png` |
| app-driver | `assets/icon/app-icon-driver-1024x1024.png` |
| app-fleet | `assets/icon/app-icon-fleet-1024x1024.png` |

Size: **1024×1024 PNG**

## Run (each app separately)

```bash
# app-rider
cd /Users/mamun/apps/with-rideshare/rideshare-mobile/app-rider
dart run flutter_launcher_icons

# app-driver
cd /Users/mamun/apps/with-rideshare/rideshare-mobile/app-driver
dart run flutter_launcher_icons

# app-fleet
cd /Users/mamun/apps/with-rideshare/rideshare-mobile/app-fleet
dart run flutter_launcher_icons
```

## What it generates

`android/app/src/main/res/mipmap-*/ic_launcher.png` — all sizes auto-generated from source PNG.
