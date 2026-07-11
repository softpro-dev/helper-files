
# How to linkup, keystore file(e.g. keystore.jks) in mobile apps
# File paths
app-driver/android/app/build.gradle.kts
app-fleet/android/app/build.gradle.kts
app-rider/android/app/build.gradle.kts


# Code of file

signingConfigs {
    create("release") {
        keyAlias = "upload"
        keyPassword = "SoftPro@26"
        storeFile = file("/Users/mamun/af-ride-keystores/keystore.jks")
        storePassword = "SoftPro@26"
    }
}