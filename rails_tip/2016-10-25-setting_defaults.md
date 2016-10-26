---
title: Setting default value for a field in rails 5
tip-number: 31
tip-username: balakarthik2011 
tip-username-profile: https://github.com/balakarthik2011
tip-description: Setting a default vaue for a field in rails 5 without using a migration.

---


We used to write a migration or a before save method for setting a default vale to a field, but in Rails 5 this has been made much easier bu using [attribute API](http://guides.rubyonrails.org/5_0_release_notes.html)
you can mention the default value of the attribute as

```ruby
    class User < ApplicationRecord
        attribute :status, default: "registered"
    end
```

```ruby
User.new => #<User id: nil, first_name: nil, last_name: nil, user_name: nil, email: nil, status: "registered">
```
