# Authentication & Security 

## 1) Cookie authentication strategy for Passport

This module lets you authenticate HTTP requests using cookies, it only allows you to recover the content of a cookie.

By plugging into Passport, bearer token support can be easily and unobtrusively integrated into any application or framework that supports Connect-style middleware, including Express..

## Install
``` $ npm install passport-cookie ```

### Usage
Configure Strategy
The cookie authentication strategy authenticates users using a cookie. The strategy requires a verify callback, which accepts that credential and calls done providing a user.

```passport.use(new CookieStrategy(
  function(token, done) {
    User.findByToken({ token: token }, function(err, user) {
      if (err) { return done(err); }
      if (!user) { return done(null, false); }
      return done(null, user);
    });
  }
));
```

## You can pass the following options to the CookieStrategy:
```
- `cookieName`: Cookie name (defaults to "token")
- `signed`: Are the cookie signed? (defaults to false)
- `passReqToCallback`: when `true`, `req` is the first argument to the verify callback (default: `false`)
```
```
passport.use(new CookieStrategy({
  cookieName: 'auth',
  signed: true,
  passReqToCallback: true
}, function(req, token, done) {
  User.findByToken({ token: token }, function(err, user) {
    if (err) { return done(err); }
    if (!user) { return done(null, false); }
    return done(null, user);
  });
})
```

## Authenticate Requests
Use passport.authenticate(), specifying the 'cookie' strategy, to authenticate requests. Requests containing cookies do not require session support, so the session option can be set to false.

For example, as route middleware in an Express application:

```
app.get("/profile",
  passport.authenticate("cookie", { session: false }),
  function(req, res) {
    res.json(req.user);
  });
  ```
## Tests
```
$ npm install
$ npm test
```
## Thanks
Thanks to Jared Hanson for his great Passport






















OAuth 2.0 & Implementation of Sign In with Google
