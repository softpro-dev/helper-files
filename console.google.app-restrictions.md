# GO: https://console.cloud.google.com/apis/credentials?project=af-ride-v1

# Add app restrictions with app id

- rider	    com.rfride.android.rider
- rider	    com.rfride.ios.rider

- driver	com.rfride.android.driver
- driver	com.rfride.ios.driver

- fleet	    com.rfride.android.fleetowner
- fleet	    com.rfride.ios.fleetowner

# Run any path in terminal (not for any specific app or path)

``` bash
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