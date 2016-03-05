---
title: Rails 5 http_cache_forever 
tip-number: 23
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: When response does not change then we want browsers and proxies to cache it for a long time. Method http_cache_forever allows us to set response headers to tell broswers and proxies that response has not modified.

---


Rails 5 allows to cache HTTP responses forever by introducting http_cache_forever method.

Sometimes, we have static pages that never/rarely change.

```ruby
  # app/controllers/home_controller.rb
  class HomeController < ApplicationController
    def index
      render
    end
  end

  # app/views/home/index.html.erb
  <h1>Welcome</h1>
```

Let’s see log for the above action.

```ruby
Processing by HomeController#index as HTML
  Rendered home/index.html.erb within layouts/application (1.3ms)
Completed 200 OK in 224ms (Views: 212.4ms | ActiveRecord: 0.0ms)
```ruby

And so on for every request for this action.

There is no change in the response and still we are rendering same thing again and again and again.

Rails 5 introduces http_cache_forever

When response does not change then we want browsers and proxies to cache it for a long time.

Method http_cache_forever allows us to set response headers to tell broswers and proxies that response has not modified.

```ruby
  # app/controllers/home_controller.rb
  class HomeController < ApplicationController
    def index
      http_cache_forever(public: true, version: 'v1') {}
    end
  end

  # OR
  class HomeController < ApplicationController
    def index
      http_cache_forever(public: true, version: 'v1') do
        render
      end
    end
  end


  # app/views/home/index.html.erb
  <h1>Welcome</h1>
```

Now let’s look at the log for the modified code.

When request is made for the first time.

```ruby
Processing by HomeController#index as HTML
  Rendered home/index.html.erb within layouts/application (1.3ms)
Completed 200 OK in 224ms (Views: 212.4ms | ActiveRecord: 0.0ms)
```

For consecutive requests for the same page

```ruby
Processing by HomeController#index as HTML
Completed 304 Not Modified in 2ms (ActiveRecord: 0.0ms)
```

On first hit, we serve the request normally but, then on each subsequent request cache is revalidated and a “304 Not Modified” response is sent to the browser.

