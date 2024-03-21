***CommandLine to follow***


**Configure dependencies**

$ flutter pub add firebase_core

$ flutter pub add firebase_auth

$ flutter pub add cloud_firestore

$ flutter pub add provider

$flutter pub add firebase_ui_auth

**Install the FlutterFire CLI**

$ dart pub global activate flutterfire_cli

$ flutterfire configure




**Cloud FireStore Rule**

rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /guestbook/{entry} {
      allow read: if request.auth.uid != null;
      allow write:
      if request.auth.uid == request.resource.data.userId
          && "name" in request.resource.data
          && "text" in request.resource.data
          && "timestamp" in request.resource.data;
          
      }
      match /attendees/{userId} {
      allow read: if true;
      allow write: if request.auth.uid == userId
          && "attending" in request.resource.data;
    }
  }
}


