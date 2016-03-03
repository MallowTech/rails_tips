---
title: show exception in format as they were requested in rails 5 
tip-number: 20
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: In rails when an exception occurs, we throw the response in html format and with this feature added the error will be thrown in the format of which the request was made.

---

Rails 5 has introduced new configuration to respond with proper format for exceptions.

```ruby
# config/environments/development.rb
config.debug_exception_response_format = :api
```

Let’s see an example of the response received with this configuration.

```ruby
$ curl localhost:3000/posts.json
{"status":404,"error":"Not Found","exception":"#\u003cActionController::RoutingError: No route matches [GET] \"/posts.json\"\u003e","traces":{"Application Trace":[...],"Framework Trace":[...]}}
```

The status key will represnt HTTP status code and error key will represent the corresponding Rack HTTP status.

exception will print the output of actual exception in inspect format.

traces will contain application and framework traces similar to how they are displayed in HTML error page.

By default, config.debug_exception_response_format is set to :api so as to render responses in the same format as requests.

If you want the original behavior of renndering HTML pages, you can configure this option as follows.

```ruby
# config/environments/development.rb
config.debug_exception_response_format = :default
```