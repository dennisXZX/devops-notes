## Firebase

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
