---
title: redirect_back with fallback location
tip-number: 18
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: We can redirect to the previous page using redirect_back and avoid HTTP_REFERER error using fallback location instead of rescue

---

In Rails 4.x, for going back to previous page we use redirect_to :back.

However sometimes we get ActionController::RedirectBackError exception when HTTP_REFERER is not present.

To avoid this exception we can use rescue and redirect to root url.

```ruby
  class PostsController < ApplicationController
    rescue_from ActionController::RedirectBackError, with: :redirect_to_default

    def publish
      post = Post.find params[:id]
      post.publish!
      redirect_to :back
    end

    private

    def redirect_to_default
      redirect_to root_path
    end
  end
```

In Rails 5, redirect_to :back has been deprecated and instead a new method has been added called redirect_back.

To deal with the situation when HTTP_REFERER is not present, it takes required option fallback_location.

```ruby
  class PostsController < ApplicationController

    def publish
      post = Post.find params[:id]
      post.publish!

      redirect_back(fallback_location: root_path)
    end
  end
```

This redirects to HTTP_REFERER when it is present and when HTTP_REFERER is not present then redirects to whatever is passed as fallback_location.