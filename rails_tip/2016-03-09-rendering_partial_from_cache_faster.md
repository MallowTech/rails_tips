---
title: Render partial from cache substantially faster
tip-number: 27
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: We render partial and below is the method that explains briefly about how to render partial faster.

---

Let’s have a look at Rails view code that renders partial using a collection.

```ruby
# index.html.erb
<%= render partial: 'todo', collection: @todos %>

# _todo.html.erb
<% cache todo do %>
  <%= todo.name %>
<% end %>
```

In the above case Rails will do one fetch from the cache for each todo.

Fetch is usually pretty fast with any caching solution, however, one fetch per todo can make the app slow.

Gem multi_fetch_fragments fixed this issue by using read_multi api provided by Rails.

In a single call to cache, this gem fetches all the cache fragments for a collection. The author of the gem saw 78% speed improvement by using this gem.

The features of this gem have been folded into Rails 5.

To get benefits of collection caching, just add cached: true as shown below.

```ruby
# index.html.erb
<%= render partial: 'todo', collection: @todos, cached: true %>

# _todo.html.erb
<% cache todo do %>
  <%= todo.name %>
<% end %>
```

With cached: true present, Rails will use read_multi to the cache store instead of reading from it every partial.

Rails will also log cache hits in the logs as below.

```ruby
Rendered collection of todos/_todo.html.erb [100 / 100 cache hits] (339.5ms)
```
