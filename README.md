# @joshforisha/cycle-firebase

[![build](https://img.shields.io/travis/joshforisha/cycle-firebase.svg?maxAge=2592000?style=flat-square)](https://travis-ci.org/joshforisha/cycle-firebase)
[![npm](https://img.shields.io/npm/v/@joshforisha/cycle-firebase.svg?maxAge=2592000?style=flat-square)](https://www.npmjs.com/package/@joshforisha/cycle-firebase)

A [Firebase v4](https://firebase.google.com/) driver for [Cycle.js](http://cycle.js.org).

## API

* [`firebaseActions`](#firebaseActions)
* [`makeFirebaseDriver`](#makeFirebaseDriver)

### <a id="firebaseActions">firebaseActions</a>

Any write effects to the connected Firebase database should be requested by calling an _action generator_&mdash;a function defined on the `firebaseActions` object&mdash;and passed to the `firebase` sink. All errors generated by actions are emitted on the [`errors`](#errors) stream.

The following action generators are defined:

* [`applyActionCode`](#firebaseActions.applyActionCode)
* [`confirmPasswordReset`](#firebaseActions.confirmPasswordReset)
* [`createUserWithEmailAndPassword`](#firebaseActions.createUserWithEmailAndPassword)
* [`goOffline`](#firebaseActions.goOffline)
* [`goOnline`](#firebaseActions.goOnline)
* [`push`](#firebaseActions.push)
* [`remove`](#firebaseActions.remove)
* [`sendPasswordResetEmail`](#firebaseActions.sendPasswordResetEmail)
* [`setPriority`](#firebaseActions.setPriority)
* [`setWithPriority`](#firebaseActions.setWithPriority)
* [`set`](#firebaseActions.set)
* [`signInAnonymously`](#firebaseActions.signInAnonymously)
* [`signInWithCredential`](#firebaseActions.signInWithCredential)
* [`signInWithCustomToken`](#firebaseActions.signInWithCustomToken)
* [`signInWithEmailAndPassword`](#firebaseActions.signInWithEmailAndPassword)
* [`signInWithPopup`](#firebaseActions.signInWithPopup)
* [`signOut`](#firebaseActions.signOut)
* [`transaction`](#firebaseActions.transaction)
* [`update`](#firebaseActions.update)

#### <a id="firebaseActions.applyActionCode"></a> `firebaseActions.applyActionCode (code)`

* `code: string`

#### <a id="firebaseActions.createUserWithEmailAndPassword"></a> `firebaseActions.createUserWithEmailAndPassword (email, password)`

* `email: string`
* `password: string`

Informs the driver to call [`firebase.auth.Auth.createUserWithEmailAndPassword()`](https://firebase.google.com/docs/reference/js/firebase.auth.Auth#createUserWithEmailAndPassword). Any errors generated by this call are emitted on the [`error` stream](#error).

#### <a id="firebaseActions.goOffline"></a> `firebaseActions.goOffline ()`

#### <a id="firebaseActions.goOnline"></a> `firebaseActions.goOnline ()`

#### <a id="firebaseActions.push"></a> `firebaseActions.push (path, value)`

* `path: string`
* `value: any`

Informs the driver to call [`firebase.database.Reference.push()`](https://firebase.google.com/docs/reference/js/firebase.database.Reference#push). Any errors generated by this call are emitted on the [`error` stream](#error).

#### <a id="firebaseActions.remove"></a> `firebaseActions.remove(path)`

Informs the driver to call [`firebase.database.Reference.remove()`](https://firebase.google.com/docs/reference/js/firebase.database.Reference#remove). Any errors generated by this call are emitted on the [`error` stream](#error).

#### <a id="firebaseActions.sendPasswordResetEmail"></a> `firebaseActions.sendPasswordResetEmail(email)`

* `email: string`

#### <a id="firebaseActions.set"></a> `firebaseActions.set(path, values)`

Informs the driver to call [`firebase.database.Reference.set()`](https://firebase.google.com/docs/reference/js/firebase.database.Reference#set). Any errors generated by this call are emitted on the [`error` stream](#error).

#### <a id="firebaseActions.setPriority"></a> `firebaseActions.setPriority(path, priority)`

* `path: string`
* `priority: (string | null | number)`

#### <a id="firebaseActions.setWithPriority"></a> `firebaseActions.setWithPriority(path, newVal, newPriority)`

* `path: string`
* `newVal: any`
* `newPriority: (string | null | number)`

#### <a id="firebaseActions.signInAnonymously"></a> `firebaseActions.signInAnonymously()`

#### <a id="firebaseActions.signInWithCredential"></a> `firebaseActions.signInWithCredential(credential)`

* `credential: firebase.auth.AuthCredential`

#### <a id="firebaseActions.signInWithCustomToken"></a> `firebaseActions.signInWithCustomToken(token)`

* `token: string`

#### <a id="firebaseActions.signInWithEmailAndPassword"></a> `firebaseActions.signInWithEmailAndPassword(email, password)`

* `email: string`
* `password: string`

Informs the driver to call [`firebase.auth.Auth.signInWithEmailAndPassword()`](https://firebase.google.com/docs/reference/js/firebase.auth.Auth#signInWithEmailAndPassword). Any errors generated by this call are emitted on the [`error` stream](#error).

#### <a id="firebaseActions.signInWithPopup"></a> `firebaseActions.signInWithPopup(provider)`

* `provider: firebase.auth.AuthProvider`

Informs the driver to call [`firebase.auth.Auth.signInWithPopup()`](https://firebase.google.com/docs/reference/js/firebase.auth.Auth#signInWithPopup). Any errors generated by this call are emitted on the [`error` stream](#error).

#### <a id="firebaseActions.signOut"></a> `firebaseActions.signOut()`

Informs the driver to call [`firebase.auth.Auth.signOut()`](https://firebase.google.com/docs/reference/js/firebase.auth.Auth#signOut). Any errors generated by this call are emitted on the [`error` stream](#error).

#### <a id="firebaseActions.transaction"></a> `firebaseActions.transaction(path, updateFn)`

* `path: string`
* `transactionUpdate: (value: any) => any`

Informs the driver to call [`firebase.database.Reference.transaction()`](https://firebase.google.com/docs/reference/js/firebase.database.Reference#transaction). Any errors generated by this call are emitted on the [`error` stream](#error).

The `updateFn` should accept and return a reference's value object.

#### <a id="firebaseActions.update"></a> `firebaseActions.update(path, values)`

* `path: string`
* `values: any`

Informs the driver to call [`firebase.database.Reference.update()`](https://firebase.google.com/docs/reference/js/firebase.database.Reference#update). Any errors generated by this call are emitted on the [`error` stream](#error).

### <a id="makeFirebaseDriver"></a> `makeFirebaseDriver(options, name)`

* `options: Config`
  * `apiKey: string`
  * `authDomain: string`
  * `databaseURL: string`
  * `storageBucket: string`
* `name?: string`

Initializes a connection to a Firebase database by calling [`firebase.initializeApp()`](https://firebase.google.com/docs/reference/js/firebase#.initializeApp), returning a source object containing the following:

* [`auth.authStateChanges`](#auth.authStateChanges)
* [`auth.idTokenChanges`](#auth.idTokenChanges)
* [`auth.providersForEmail`](#auth.providersForEmail)
* [`auth.redirectResults`](#auth.redirectResults)
* [`database.ref()`](#database.ref)
* [`errors`](#errors)

#### <a id="auth.authStateChange"></a> `auth.authStateChange`

A stream based on the output of [`firebase.auth.Auth.onAuthStateChanged()`](https://firebase.google.com/docs/reference/js/firebase.auth.Auth#onAuthStateChanged).

#### <a id="auth.idTokenChanges"></a> `auth.idTokenChanges`

A stream based on the output of [`firebase.auth.Auth.onIdTokenChanged()`](https://firebase.google.com/docs/reference/js/firebase.auth.Auth#onIdTokenChanged).

#### <a id="auth.providersForEmail"></a> `auth.providersForEmail(email)`

* `email: string`

Returns a stream based on the output of [`firebase.auth.Auth.fetchProvidersForEmail()`](https://firebase.google.com/docs/reference/js/firebase.auth.Auth#fetchProvidersForEmail).

#### <a id="auth.authStateChanges"></a> `auth.authStateChanges`

A stream based on the output of [`firebase.auth.Auth.onAuthStateChanged()`](https://firebase.google.com/docs/reference/js/firebase.auth.Auth#onAuthStateChanged).

#### <a id="database.ref"></a> `database.ref(path)`

Returns a stream of the ref's `eventType` values at `path`, by utilizing [`firebase.database.Reference.on()`](https://firebase.google.com/docs/reference/js/firebase.database.Reference#on).

#### <a id="errors"></a> `errors`

A stream of errors generated by the defined [firebaseActions](#firebaseActions).
