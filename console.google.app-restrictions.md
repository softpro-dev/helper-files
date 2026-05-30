# GO: https://console.cloud.google.com/apis/credentials/key/8017e3c7-5afc-4d85-bd4c-9296e4b98ed0?authuser=2&project=a5-ride-share

# Add app restrictions with app id

- rider	    com.rfride.android.rider
- rider	    com.rfride.ios.rider

- driver	com.rfride.android.driver
- driver	com.rfride.ios.driver

- fleet	    com.rfride.android.fleetowner
- fleet	    com.rfride.ios.fleetowner

# Run any path in terminal (not for any specific app or path)
## Eta SHA-1(fingerprint) ready kore

``` bash
keytool -list -v -keystore ~/.android/debug.keystore -alias androiddebugkey -storepass android -keypass android | grep SHA1

```

## To generate new SHA-1(fingerprint) 
``` bash
keytool -genkey -v -keystore ~/.android/debug.keystore -alias androiddebugkey -keyalg RSA -keysize 2048 -validity 10000 -storepass android -keypass android -dname "CN=Android Debug,O=Android,C=US"

# then abar read koro (first command)
keytool -list -v -keystore ~/.android/debug.keystore -alias androiddebugkey -storepass android -keypass android | grep SHA1

```
Outut Example: F3:0D:3D:8F:F1:36:80:AC:AC:FF:30:03:AC:61:89:D3:87:82:DC:A3
This fingerpring copy and paste their



# Maps API key-এর জন্য এগুলো select করো:

Maps SDK for Android
Maps SDK for iOS (যদি same key use করো)
Directions API (route/navigation)
Distance Matrix API (distance calculation)
Geocoding API (address → coordinates)
Places API (location search, autocomplete)


# Example in image (app-restriction.example.png)