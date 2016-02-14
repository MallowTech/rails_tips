---
title: Efficiency of pluck 
tip-number: 03
tip-username: logesh 
tip-username-profile: https://github.com/logeshmallow
tip-description: Pluck can be used to select one or more attributes without loading a bunch of records just to grab the attributes you want.

---

We often come through the requirement of selecting a particular attribute or few attributes and we use few methods to do this like pluck, select and map/collect and we are not certain on how efficient are those.

##map/collect with select:

Basically these 2 methods are alias of each other, thus they do one and the same thing.

```ruby
User.select(:id).collect(&:id) 
User.select(:id).map(&:id)
User Load (0.5ms)  SELECT "users"."id" FROM "users"
Benchmark.ms{User.select(:id).collect(&:id)} => 1.824394003051566
```

##pluck:

Can be used to select one or more attributes without loading a bunch of records just to grab the attributes you want.

```ruby
User.pluck(:id)
(0.5ms)  SELECT "users"."id" FROM "users"
Benchmark.ms{User.pluck(:id)} => 1.1335880008118693
```

We can select multiple attributes by using both these but here is the difference

```ruby
Benchmark.ms{User.select(:id, :email).collect{|x| [x.id, x.email]}}
  User Load (0.5ms)  SELECT "users"."id", "users"."email" FROM "users"
=> 1.79159800245543
```

```ruby
Benchmark.ms{User.pluck(:id, :email)}                             
(0.5ms)  SELECT "users"."id", "users"."email" FROM "users"
=> 1.2821059972338844
```

The SQL query executed in both the cases is exactly the same, but time taken by pluck approach is considerably less than that of collect/map with select.

I hope the above tip will be useful.
