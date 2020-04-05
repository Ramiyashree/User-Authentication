# Authentication & Security 

Using Passport.js to Add Cookies and Sessions

Cookie authentication strategy for Passport

This module lets you authenticate HTTP requests using cookies, it only allows you to recover the content of a cookie.

By plugging into Passport, bearer token support can be easily and unobtrusively integrated into any application or framework that supports Connect-style middleware, including Express..

Install
$ npm install passport-cookie
Usage
Configure Strategy
The cookie authentication strategy authenticates users using a cookie. The strategy requires a verify callback, which accepts that credential and calls done providing a user.

passport.use(new CookieStrategy(
  function(token, done) {
    User.findByToken({ token: token }, function(err, user) {
      if (err) { return done(err); }
      if (!user) { return done(null, false); }
      return done(null, user);
    });
  }
));
Authenticate Requests
Use passport.authenticate(), specifying the 'cookie' strategy, to authenticate requests. Requests containing cookies do not require session support, so the session option can be set to false.

For example, as route middleware in an Express application:

app.get("/profile",
  passport.authenticate("cookie", { session: false }),
  function(req, res) {
    res.json(req.user);
  });
  
  
OAuth 2.0 & Implementation of Sign In with Google
