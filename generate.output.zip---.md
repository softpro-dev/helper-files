
# URL: https://play.google.com/console/u/2/developers/6642512590822881334/app/4974723767820690727/tracks/4701196743142224525/releases/7/prepare


Open a terminal in ~/Downloads
Files
- pepk.jar
- encryption_public_key.pem

```bash
java -jar pepk.jar --keystore=/Users/mamun/afride-upload-key.jks --alias=upload --output=output.zip --include-cert --rsa-aes-encryption --encryption-key-path=encryption_public_key.pem
```

password: SoftPro@26
password: SoftPro@2026