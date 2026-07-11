# Google Play Upload Key Reset - Step-by-Step Guide

**Source:** Google Play Developer Support (Jul 3, 2026)

---

## Prerequisites
- You must be the account owner to request an upload key reset
- The reset request must be done via Google Play Console
- New upload key must be 2048-bit RSA with 25-year validity

---

## Step 1: Generate New Upload Key

Run this command to create a new keystore:

```bash
keytool -genkeypair -alias upload -keyalg RSA -keysize 2048 -validity 9125 -keystore keystore.jks
```

**Note:** 9125 days = 25 years (2048-bit RSA requirement)

---

## Step 2: Export Certificate to PEM Format

Export the certificate from the keystore:

```bash
keytool -export -rfc -alias upload -file upload_certificate.pem -keystore keystore.jks
```

When prompted, enter the keystore password.

---

## Step 3: Request Upload Key Reset in Play Console

1. Go to your app in Google Play Console
2. Select **"Protected with Play"** section
3. Click **"Play Store protection"** → **"Manage Play app signing"**
4. Go to **"Upload Key Certificate"** section
5. Click **"Request Upload key reset"**
6. Provide a reason why you're requesting the reset
7. Enter the PEM file contents (paste contents of `upload_certificate.pem`)
8. Click **"Request"**

---

## Step 4: Wait for Google's Processing

- Google will process the request
- **Wait at least 48 hours** before attempting to upload with the new key
- Do NOT upload with the new key until Google confirms the reset

---

## Step 5: Configure App to Use New Key

Once Google confirms the reset (check email):

1. Update Gradle signing config to use new keystore
2. Rebuild APK/AAB with new key
3. Upload to Play Console

---

## Files Generated
- `keystore.jks` — New keystore (store securely, don't lose it!)
- `upload_certificate.pem` — Certificate for Play Console upload key reset request

---

## Timeline
- **Now:** Generate key + export certificate
- **Now:** Submit reset request to Google
- **48 hours later:** Check email for Google's confirmation
- **After confirmation:** Update build config + upload new AAB

---

## Important Notes
- Keep `keystore.jks` in a secure location (backup it!)
- The upload key is different from the app signing key
- All future uploads must use this new key
- Users must reinstall the app (different signing cert = different app identity)
