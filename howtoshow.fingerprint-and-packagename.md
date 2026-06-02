

# show finger print
``` bash  
keytool -list -v -keystore ~/.android/debug.keystore -alias androiddebugkey -storepass android -keypass android
``` 
# Show package-name
## each app directory, then run
``` bash
grep "applicationId" android/app/build.gradle.kts
```
 