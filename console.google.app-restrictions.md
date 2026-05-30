# GO: https://console.cloud.google.com/apis/credentials?project=af-ride-v1


- rider	    com.rfride.android.rider
- rider	    com.rfride.ios.rider

- driver	com.rfride.android.driver
- driver	com.rfride.ios.driver

- fleet	    com.rfride.android.fleetowner
- fleet	    com.rfride.ios.fleetowner

keytool -list -v -keystore ~/.android/debug.keystore -alias androiddebugkey -storepass android -keypass android | grep SHA1


# Example in image (app-restriction.example.png)