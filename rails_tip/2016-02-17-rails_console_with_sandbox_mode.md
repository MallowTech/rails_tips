---
title: Run rails console in sandbox mode
tip-number: 06
tip-username: prakash 
tip-username-profile: https://github.com/prakashROR
tip-description: In sandbox mode, any database changes made while in the console will be reverted when you exit the console.
---

This feature comes in handy any time we need to run methods from the console without permanently changing data.
For example, when trying to reproduce reported bugs in production, we can use the sandbox mode to make sure we don’t accidentally change existing user data.

```ruby
rails c --sandbox
Loading development environment in sandbox (Rails 5.0.0.beta2)
Any modifications you make will be rolled back on exit
2.3.0 :001 > User.count
   (0.7ms)  SELECT COUNT(*) FROM "users"
 => 10 
2.3.0 :002 >  User Load (1.0ms)  SELECT "users".* FROM "users"
   (0.2ms)  SAVEPOINT active_record_1
  SQL (0.6ms)  DELETE FROM "users" WHERE "users"."id" = $1  [["id", 14]]
   (0.1ms)  RELEASE SAVEPOINT active_record_1
   (0.1ms)  SAVEPOINT active_record_1
  SQL (0.4ms)  DELETE FROM "users" WHERE "users"."id" = $1  [["id", 15]]
   (0.1ms)  RELEASE SAVEPOINT active_record_1
   (0.1ms)  SAVEPOINT active_record_1
  SQL (0.4ms)  DELETE FROM "users" WHERE "users"."id" = $1  [["id", 18]]
   (0.2ms)  RELEASE SAVEPOINT active_record_1
   (0.1ms)  SAVEPOINT active_record_1
  SQL (0.4ms)  DELETE FROM "users" WHERE "users"."id" = $1  [["id", 19]]
   (0.1ms)  RELEASE SAVEPOINT active_record_1
   (0.1ms)  SAVEPOINT active_record_1
  SQL (0.4ms)  DELETE FROM "users" WHERE "users"."id" = $1  [["id", 24]]
   (0.2ms)  RELEASE SAVEPOINT active_record_1
   (0.1ms)  SAVEPOINT active_record_1
  SQL (0.3ms)  DELETE FROM "users" WHERE "users"."id" = $1  [["id", 1]]
   (0.2ms)  RELEASE SAVEPOINT active_record_1
   (0.1ms)  SAVEPOINT active_record_1
  SQL (0.3ms)  DELETE FROM "users" WHERE "users"."id" = $1  [["id", 25]]
   (0.1ms)  RELEASE SAVEPOINT active_record_1
   (0.2ms)  SAVEPOINT active_record_1
  SQL (0.4ms)  DELETE FROM "users" WHERE "users"."id" = $1  [["id", 27]]
   (0.1ms)  RELEASE SAVEPOINT active_record_1
   (0.2ms)  SAVEPOINT active_record_1
  SQL (0.3ms)  DELETE FROM "users" WHERE "users"."id" = $1  [["id", 26]]
   (0.1ms)  RELEASE SAVEPOINT active_record_1
   (0.1ms)  SAVEPOINT active_record_1
  SQL (0.3ms)  DELETE FROM "users" WHERE "users"."id" = $1  [["id", 28]]
   (0.1ms)  RELEASE SAVEPOINT active_record_1
[...]
2.3.0 :003 > User.count
   (0.4ms)  SELECT COUNT(*) FROM "users"
 => 0 
2.3.0 :004 > exit
   (0.3ms)  ROLLBACK 
```


Hope this is useful..
