# Passport-NUS-OpenID

[![NPM version](https://badge.fury.io/js/passport-nus-openid.svg)](http://badge.fury.io/js/passport-nus-openid)

[Passport](http://passportjs.org/) strategy for authenticating with [NUS](http://www.nus.edu.sg/)
using OpenID 2.0.

This module lets you authenticate using NUSNET in your Node.js applications.
By plugging into Passport, nus authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Install

    $ npm install passport-nus-openid

## Usage

#### Configure Strategy

The NUS authentication strategy authenticates users using an NUSNET account,
which is also an OpenID 2.0 identifier.  The strategy requires a `verify`
callback, which accepts this identifier and calls `done` providing a user.
Additionally, options can be supplied to specify a return URL and realm.

    passport.use(new NusStrategy({
        returnURL: 'http://localhost:3000/auth/nus/return',
        realm: 'http://localhost:3000/'
      },
      function(identifier, done) {
        User.findByOpenID({ openId: identifier }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'NUS'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/nus',
      passport.authenticate('nus'));

    app.get('/auth/nus/return', 
      passport.authenticate('nus', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });
      
## Credits

  - [Jared Hanson](http://github.com/jaredhanson) ([passport-intuit](https://github.com/jaredhanson/passport-intuit))

## License

[The MIT License](http://opensource.org/licenses/MIT)
