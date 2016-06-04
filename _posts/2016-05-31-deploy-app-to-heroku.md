---
layout: post
title:  "How to deploy a Node app to Heroku"
date:   2016-05-31 11:57:24 -04:00
tags: ['Coding','Heroku', 'Node']
---

Once you [signed up for a free account][1] and installed the [heroku toolbelt][2], there are just a few commands you need to run in the Terminal to deploy your Node app. But before that, you'll need to tweak a few things in your app to make it work with Heroku.

Add a new `start` script to your `package.json` file. For instance, if you run `node server.js` to run your app locally, then your script should look like that:

```json
"scripts": {
  "start": "node server.js"
}
```

In that `server.js` file, you'll want to make sure you tell your app which port to bind to using the node environment variable Heroku provides. Something like that should do the trick:

```javascript
var express = require('express');

var app = express();
const PORT = process.env.PORT || 3000; // <= here

app.use(express.static('public'));

app.listen(PORT, function() {
  console.log('Express server running on port: ' + PORT);
});
```

Once your app is all setup, the rest is pretty easy. Head over to your Terminal and run those:

1. `heroku login` - enter the credentials you used to sign up
2. `heroku auth:whoami` - to check you're indeed logged in heroku toolbelt
3. `heroku create` - to add a new remote to your git repo with the custom URL where heroku is hosting your app (make sure you're inside the right git repo first…)
4. `git remote -v` - to check the heroku remote was added successfully
5. `git push heroku master` - to push your `master` branch to heroku
6. `heroku open` - to open that new heroku URL in your browser
7. Done! :)


[1]:https://signup.heroku.com
[2]:https://toolbelt.heroku.com
