## Firebase

#### Firestore

A query is a request we make to firestore to give us something from the database. Firestore returns us two types of objects: references and snapshots. Of these objects, they can be either `Document` or `Collection` versions. Firestore will __always__ return us these objects, even if nothing exists at from that query.

A queryReference object is an object that represents the current place in the database that we are querying.

We get them by calling either:
 - firestore.doc('/users/:userId')
 - firestore.collection('/users')
 
The queryReference object does not have the actual data of the collection or document. It instead has properties that tell us details about it, or the method to get the Snapshot object which gives us the data we are looking for.

We use documentRef objects to perform CRUD methods (`.set()`, `.get()`, `.update()`, `.delete()`). We can also add documents to collections using the collectionRef object using `.add()` method.

We get the snapshotObject from referenceObject using the `.get()` method.
  - documentRef.get() returns a queryDocumentSnapshot object
  - collectionRef.get() returns a collectionSnapshot object

#### Database authentication

You can config authentication in the database rules, so each properties can be set for its read and write permissions.

```
{
  "rules": {
      "ingredients": {
        ".read": "true",
        ".write": "true"
      },
      "orders": {
        ".read": "auth != null",
        ".write": "auth != null",
          ".indexOn": ["userId"]
      }
  }
}
```

#### Host an React app on Firebase

- Run `npm run build` to generate a production build
- Go to Firebase hosting and follow the instructions of installing `firebase-tools` 
- Run `firebase login` to login
- Initalize a firebase project by running `firebase init`
  - you will be prompted to set your public directory
  - whether to configure as a single-page app
  - whether to overwrite the index.html
- You can find your deploy config in `firebase.json`
- Run `firebase deploy` to deploy your app
