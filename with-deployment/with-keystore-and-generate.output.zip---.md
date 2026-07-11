
# URL: https://play.google.com/console/u/2/developers?pli=1

Open a terminal in /Users/mamun/af-ride-keystores
Files
- keystore-path: /Users/mamun/af-ride-keystores/keystore.jks


# How create new Keystore(If needed)
keytool -genkey -v -keystore /Users/mamun/af-ride-keystores/keystore.jks -keyalg RSA -keysize 2048 -validity 10950 -alias upload

password: SoftPro@26
What is your first and last name?                   AF Ride
What is the name of your organizational unit?       ATLAS FABULOSO LDA
What is the name of your organization?              ATLAS FABULOSO LDA
What is the name of your City or Locality?          Lisbon
What is the name of your State or Province?         Portugal
What is the two-letter country code for this unit?  PT


# Ready project with keystore(.jks) file 
## for app:driver
```bash
cat > ~/apps/with-rideshare/rideshare-mobile/app-driver/android/key.properties << EOF
storeFile=~/afride-upload-key-new.jks
storePassword=SoftPro@26
keyPassword=SoftPro@26
keyAlias=upload
EOF
```