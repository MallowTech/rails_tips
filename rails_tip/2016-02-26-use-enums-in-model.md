---
title: Use enums in models
tip-number: 15
tip-username: Jayaprakash
tip-username-profile: https://github.com/JPMallow
tip-description: How to use enums in Rails models?

---

###enums

Advantage:
The column in the database can be integer type, but can access that column through enum.

```ruby
Class Task < ActiveRecord::Base
  enum status: { to_do: 0, in_progress: 1, completed: 2 }
end
```

Accessing enums in controller methods

```ruby
Task.statuses[:to_do] #=> "0"
Task.statuses[:in_progress] #=> "1"
Task.statuses[:completed] #=> "2"
```

I hope this is useful.
