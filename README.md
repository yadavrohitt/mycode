rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
    match /beacons/{beaconId} {
      allow read: if request.auth != null;
      allow create, update, delete: if request.auth != null;
    }
    match /config/floorPlan {
      allow read, write: if request.auth != null;
    }
  }
}
