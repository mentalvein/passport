# Passport.js authentication for Mental Vein

[Passport](http://passportjs.org/) strategy for authenticating with [Mental Vein](http://mentalvein.com/) using the OAuth 2.0 API.

This module lets you authenticate using Mental Vein in your Node.js applications.

By plugging into Passport, Mental Vein authentication can be easily and unobtrusively integrated into any application or framework that supports [Connect](http://www.senchalabs.org/connect/)-style middleware, including [Express](http://expressjs.com/).

## Install
```
npm install passport-mentalvein
```

## Usage

#### Configure Strategy

The Mental Vein authentication strategy authenticates users using a Mental Vein account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which accepts these credentials and calls `done` providing a user, as well as `options` specifying a client ID, client secret, and callback URL.
```
var OAuth2Strategy = require("passport-mentalvein").Strategy;

passport.use(new OAuth2Strategy({
	clientID: CLIENT_ID,
	clientSecret: CLIENT_SECRET,
	callbackURL: "http://www.example.net/auth/mentalvein/callback"
	},
	function(accessToken, refreshToken, profile, done) {
	User.findOrCreate({ providerId: profile.id }, function (err, user) {
		return done(err, user);
	});
	}
));
```

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'mentalvein'` strategy, to authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/) application:

```
app.get('/auth/mentalvein',
	passport.authenticate('mentalvein'));

app.get('/auth/mentalvein/callback',
	passport.authenticate('mentalvein', { failureRedirect: '/login' }),
	function(req, res) {
	// Successful authentication, redirect home.
	res.redirect('/');
	});
```

## Credits

Initiated by [Makis Tracend](http://github.com/tracend)

Part of [Mental Vein](http://mentalvein.com/) by [K&D Interactive](http://kdi.co/)

Released under the [MIT license](http://makesites.org/licenses/MIT)

