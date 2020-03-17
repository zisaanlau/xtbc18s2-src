---
title: "Day 8: Firebase Authentication"
weight: 4
---

<date>Thursday, June 14, 2018</date>

Morning:

* [Playlist](https://www.youtube.com/watch?v=AxtgfBl_yIw&list=PLuT2TqJuwaY-wZ8GKN0bjgCwNVf1WpEGp) | [Day 8, Part 1](https://www.youtube.com/watch?v=KhLMefiLrpM&list=PLuT2TqJuwaY-wZ8GKN0bjgCwNVf1WpEGp&index=97)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=GOQvgEk9IBM&list=PLuT2TqJuwaY90mQ7meSdhHMX6FbfCaLNA) | [Day 8, Part 1](https://www.youtube.com/watch?v=FGWi2B7jWKM&index=102&list=PLuT2TqJuwaY90mQ7meSdhHMX6FbfCaLNA)

## Topics

### Firebase Authentication

* 'firebase/auth'
* `authWithPopup`
* signing in and out
* handling auth state changes
* database rules

## Examples

## Authentication

Firebase isn't just a real-time database.  It can also provide authentication services via email/password, phone, or common third-party services like Github, Facebook, and Google. For _Chatarang_, we set up authentication via Google.

### Step 1: Enable Google authentication in Firebase

Go to your Firebase console and click on the "Authentication" tab in the "Develop" sidebar, then click on "Sign-in method."  You'll see a list of the authentication methods allowed by Firebase. Click on "Google" and then enable with the toggle switch.

### Step 2: Add Firebase auth to your app

_Note: This step assumes you already have your Firebase database added to your app._ 

Import `firebase/auth` into your app's firebase setup.  Enable firebase auth and also create an instance of `GoogleAuthProvider`.

**base.js**

{{< code lang="js" line="4,17,18" class="line-numbers" >}}
import firebase from 'firebase/app'
import Rebase from 're-base'
import 'firebase/auth'
import 'firebase/database'

const app = firebase.initializeApp({
  apiKey: "YOURAPIKEY",
  authDomain: "YOURAUTHDOMAIN",
  databaseURL: "YOURDATABASEURL",
  projectId: "YOURPROJECTID",
  storageBucket: "YOURSTORAGEBUCKET",
  messagingSenderId: "YOURSENDERID"
})

const app = firebase.initializeApp(config)

export const googleProvider = new firebase.auth.GoogleAuthProvider()
export const auth = firebase.auth()

const db = app.database()
export default Rebase.createClass(db)
{{< /code >}}

### Step 3: Set up the SignIn Component

Import `auth` and the `googleProvider` into whatever component handles the sign-in process. Call `signInWithPopup` on the `auth` object, passing the provider as a parameter. This will launch a popup screen that will prompt the user to sign in using the provider you have specified.

**SignIn.js**

{{< code jsx >}}
import React, { Component } from 'react'
import { auth, googleProvider } from './base'

class SignIn extends Component {
  state = {
    email: '',
  }

  authenticate = () => {
    auth.signInWithPopup(googleProvider)
      .then(result => this.props.handleAuth(result.user))
      .catch(error => console.log(error))
  }

  render() {
    return (
      &lt;button className="SignIn" onClick={this.authenticate}&gt;
        Sign In With Google
      &lt;/button&gt;
    )
  }
}

export default SignIn
{{< /code >}}

### Step 4: Handling auth state changes (and page refreshes)

Once the user has authenticated via the popup, the state of our authorization has changed (we now have an authenticated user). Other events that can cause auth state changes are signing out, timeouts, and page refreshes.  We should probably set up something to listen for these events.  In the `componentWillMount` lifecycle hook that runs when the Component is first getting loaded, we can call the `onAuthStateChanged` method provided on the global `auth` object to set up such a listener.

**App.js**

{{< code js >}}
// ...

componentWillMount() {
    const user = JSON.parse(localStorage.getItem('user'))

    if (user) {
      this.setState({ user })
    }

    auth.onAuthStateChanged(
      user => {
        if (user) {
          this.handleAuth(user)
        } else {
          this.handleUnauth()
        }
      }
    )
  }

// ...
{{< /code >}}

#### Step 5: Finishing sign-in

What the `authHandler` callback does is up to you, but for _Chatarang_, we had it do pretty typical things - save the user ID to state, and initialize syncing our local state for 'rooms' with the data stored on Firebase.

**App.js**

{{< code js >}}
// ...

handleAuth = (oauthUser) => {
    const user = {
      email: oauthUser.email,
      uid: oauthUser.uid,
      displayName: oauthUser.displayName,
    }
    this.setState({ user })
    localStorage.setItem('user', JSON.stringify(user))
  }

// ...
{{< /code >}}

#### Step 6: Signing out

Signing out when using Firebase for authentication is also simple - just call `auth.signOut()`!

**App.js**

{{< code js >}}
// ...

 signOut = () => {
    auth.signOut()
  }

  handleUnauth = () => {
    this.setState({ user: {} })
    localStorage.removeItem('user')
  }

// ...
{{< /code >}}

### Rules

For your Firebase database, you can set up rules (written in JSON) that specify the conditions under which data is allowed to be read or written.  By default, a newly generated project will require that a user be authenticated to read or write _any_ data.

{{< code js >}}
{
  "rules": {
    ".read": "auth != null",
    ".write": "auth != null"
  }
}
{{< /code >}}

If you do not have authentication set up yet, these values can be set to `true`.  This allows _anyone_ to read or write any data in the database.  This can be convenient, but probably not a good idea long-term (and you _will_ get a warning if you do that).

Additional rules can be applied per endpoint:

{{< code js >}}
{
  "rules": {
    "emails": {
      ".read": true,
      ".write": "auth != null"
    },
    "texts": {
      ".read": true,
      ".write": "auth != null"
    },
    "users": {
      "$userId": {
        ".read": "auth != null && auth.uid == $userId",
        ".write": "auth != null && auth.uid == $userId"
      }
    }
  }
}
{{< /code >}}

The above rules translate to:

* texts and emails can be read by anyone, but only written by authenticated users
* users data can be read and written only by an authenticated user whose `uid` matches the `$userId` of that item

## Projects

* Chatarang: [Morning](https://github.com/xtbc18s2/chatarang) | [Afternoon](https://github.com/xtbc18s2/chatarang/tree/afternoon)

## Homework

* Add another authentication method (or two?). Remember, [documentation](https://firebase.google.com/docs/auth/web/manage-users#get_the_currently_signed_in_user) is your friend.

### Super Mega Bonus Credit

* Continue to enhance the app. Be creative!

### Super Mega Bonus Credit Hyper Fighting

* Have a great weekend!
