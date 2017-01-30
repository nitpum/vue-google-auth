# vue-google-auth
Handling Google sign-in and sign-out for Vue.js applications

## Installation
`npm install simmatrix/vue-google-auth`

## Initialization
```
import GoogleAuth from 'vue-google-auth'

Vue.use(GoogleAuth, { clientID: 'xxxxxxxxxx-xxxxxxxxxxxxxxxxxxxxxxxxxx.apps.googleusercontent.com' })
Vue.googleAuth().load()
```
Ideally you shall put in this in your main file, e.g. main.js

## Usage - Sign-in
###(a) Handling Google sign-in, getting the one-time authorization code from Google
```
import Vue from 'vue'

Vue.googleAuth().signIn(function (authorizationCode) { 
  // things to do when sign-in succeeds, you may send the authorizationCode to your backend server
}, function (error) {
  // things to do when sign-in fails
))
```

The `authorizationCode` that is being returned is the `one-time code` that you can send to your backend server, so that the server can exchange for its own access token and refresh token.


###(b) Alternatively, if you would like to directly get back the access_token and id_token
```
import Vue from 'vue'

// Just add in this line
Vue.googleAuth().directAccess()

Vue.googleAuth().signIn(function (googleUser) { 
  // things to do when sign-in succeeds
}, function (error) {
  // things to do when sign-in fails
))
```

The `googleUser` object that is being returned will be:
```
{
  "token_type": "Bearer",
  "access_token": "xxx",
  "scope": "xxx",
  "login_hint": "xxx",
  "expires_in": 3600,
  "id_token": "xxx",
  "session_state": {
    "extraQueryParams": {
      "authuser": "0"
    }
  },
  "first_issued_at": 1234567891011,
  "expires_at": 1234567891011,
  "idpId": "google"
}
```

## Usage - Sign-out
Handling Google sign-out
```
import Vue from 'vue'

Vue.googleAuth().signOut(function () { 
  // things to do when sign-out succeeds
}, function (error) {
  // things to do when sign-out fails
))
```

## Additional Help
If you are curious of how the entire Google sign-in flow works
![Google Sign-in Flow](http://i.imgur.com/BQPXKyT.png)