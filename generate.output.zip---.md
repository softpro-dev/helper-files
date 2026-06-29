
# URL: https://play.google.com/console/u/2/developers?pli=1

Open a terminal in ~/Downloads
Files
- keystore-path: /Users/mamun/afride-upload-key-new.jks

- pepk.jar
- encryption_public_key.pem
 
```bash
java -jar pepk.jar --keystore=keystore.jks --alias=upload --output=output.zip --include-cert --rsa-aes-encryption --encryption-key-path=encryption_public_key.pem
```

password: SoftPro@26





# How create new Keysotore(If needed)
keytool -genkey -v -keystore ~/afride-upload-key-new.jks -keyalg RSA -keysize 2048 -validity 10950 -alias upload

password: SoftPro@26
What is your first and last name?                   AF Ride
What is the name of your organizational unit?       ATLAS FABULOSO LDA
What is the name of your organization?              ATLAS FABULOSO LDA
What is the name of your City or Locality?          Lisbon
What is the name of your State or Province?         Portugal
What is the two-letter country code for this unit?  PT