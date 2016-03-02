---
title: pluck added to enumerable in rails 5 
tip-number: 20
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: Due to this addition of method, when relation is already loaded then instead of firing query with pluck, it uses Enumerable#pluck to get data.

---

### With Rails 4.x

```ruby
  users = User.all
  SELECT `users`.* FROM `users`

  users.pluck(:id, :name)
  SELECT "users"."id", "users"."name" FROM "users"

  => [[2, "Balakarthik"], [3, "Gokul"], [4, "ArunPandi"]]
```

### With Rails 5

```ruby
  users = User.all
  SELECT "users".* FROM "users"

  # does not fire any query
  users.pluck(:id, :name)
  => [[1, "Premanandh"], [2, "Balakarthik"], [3, "Gokul"]]
```
