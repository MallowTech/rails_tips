---
title: Remove nil from hash using Hash#compact and Hash#compact!
tip-number: 30
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: We always had an issue when we send hash with nil value and now here is the option in ruby 2.4 to remove the nil using Hash#compact and Hash#compact!

---




We all would have faced removing nil value from array and hash and we had compact for removing nil from array and now in ruby 2.4, we also have option to remove it from hash

```ruby
 
    hash = { "username" => "logesh", "company" => nil}
    hash.compact #=> { "username" => "logesh" }
    hash #=> { "username" => "logesh", "company" => nil}

    hash.compact! #=> { "username" => "logesh" }
    hash #=> { "username" => "logesh" }
```

Since this comes with ruby itself, we even don't need rails to use this.
