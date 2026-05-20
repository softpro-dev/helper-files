# URL
- https://console.firebase.google.com/u/0/project/af-ride-v1/settings/serviceaccounts/adminsdk


var admin = require("firebase-admin");

var serviceAccount = require("path/to/serviceAccountKey.json");

admin.initializeApp({
  credential: admin.credential.cert(serviceAccount)
});
