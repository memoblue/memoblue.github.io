---
layout: post
title:  "Firebase CRUD"
date:   2016-07-13 07:08:45 -04:00
tags: ['Coding','Database', 'API']
---

Here's an overview on how to perform basic CRUD operations with [Firebase][1].

Once you've logged in Firebase with your google account and created a new project in the console, just create a new Database and click on the "Rules" tab to change them to:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

Although these rules should not be used in a real app, it makes it easy to play with dummy data to familiarize yourself with the basics.

Go back to the project main page, click on "Add Firebase to your web app" and copy/paste that code in your local dev environment. If the `<script src>` approach is not your thing, there's also a package available: `npm install --save firebase`.

Once you got that setup, the first thing you'll want to do is add a reference to you database:

```javascript
var dbRef = firebase.database().ref();
```

## Create

`dbRef.set()` wipes any data at the ref point. It takes an object and returns a promise.

```javascript
dbRef.set({
  app: {
    name: 'My App',
    version: '1.0.0'
  },
  user: {
    name: 'memo',
    age: 102
  }
});
```

For arrays, there is a `dbRef.push()` method which creates a new ref (with an automatically generated id) to which you can add data to.

```javascript
var tags = fbRef.child('tags');
tags.push({
    'tag': 'js',
    'text': 'JavaScript'
});
```

## Read

`dbRef.once()` is only called once and it returns a promise with a "snapshot" of the ref.

```javascript
dbRef.child('app').once('value').then((snapshot) => {
    console.log('Got database', snapshot.key, snapshot.val());
}, (e) => {
    console.log('Something went wrong', e);
});
```

`dbRef.on()` is called on every database changes and takes a callback function. You can remove the listener by using `dbRef.off()`.

```javascript
var data = (snapshot) => {
    console.log('Got value', snapshot.val());
};
dbRef.on('value', data);
dbRef.off(data);
```

For arrays, there are other listeners for the `dbRef.on()` method:

* `child_added`
* `child_changed`
* `child_removed`

## Update

`dbRef.update()` works the same as `set()` but it updates **the first level** of properties instead of wiping everything (it will still wipe anything below). It takes an object and returns a promise.

```javascript
dbRef.update({
    'app/version': '1.0.1'
})
```

## Delete

You can either use `dbRef.remove()` or set a value to `null` to remove it.

```javascript
dbRef.child('app/name').remove();

dbRef.child('app').update({
    'version': '1.0.2',
    name: null
})
```

### Note: accessing different points in the database

You can use the `child()` method or a "multi path".

```javascript
dbRef.child('user').update({
    name: 'memoblue' // age is gone
});

dbRef.update({
  'user/name': 'memoblue' // multi path does not work within set()
});
```


[1]:https://firebase.google.com/
