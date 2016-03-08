---
title: Interaction with app from rails console
tip-number: 25
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: We can interact with the app from console to imitate the real user action without a browser or server

---

### Issuing Requests Interactively

The app object can also issue faux requests into your app, mimicing what a real user might do. We tend not to do this very often, but it can be quite useful for one-off interactions with the app from the console. The best part is that no browser or server is required.

Here's a quick test drive to give you a feel for what's possible:

```ruby
>> app.get "/movies"
=> 200

>> app.get "/users/1"
=> 302

>> app.response.redirect_url
=> "http://www.example.com/session/new"

>> app.post "/session", email: 'fred@example.com', password: 'secret'
=> 302

>> app.response.redirect_url
=> "http://www.example.com/users/1"

>> app.session[:user_id]
=> 7
```

For more details on the methods you can call on the app object to issue requests, check out the ActionDispatch::Integration::RequestHelpers documentation.
