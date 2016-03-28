---
title: Support for left outer join in Rails 5
tip-number: 28
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: In rails whenever we were supposed to use left outer join, we use raw sql instead of active record way and rails 5 has provided support to left outer join in active record way

---

In Rails 4.x, we need to write the SQL for left outer join mnually as Active Record does not have support for outer joins.

```ruby
authors = Author.join('LEFT OUTER JOIN "posts" ON "posts"."author_id" = "authors"."id"')
                .uniq
                .select("authors.*, COUNT(posts.*) as posts_count")
                .group("authors.id")
```

Rails 5 has added left_outer_joins method.

```ruby
authors = Author.left_outer_joins(:posts)
                .uniq
                .select("authors.*, COUNT(posts.*) as posts_count")
                .group("authors.id")
```

It also allows to perform the left join on multiple tables at the same time.

```ruby
>> Author.left_joins :posts, :comments
  Author Load (0.1ms)  SELECT "authors".* FROM "authors" LEFT OUTER JOIN "posts" ON "posts"."author_id" = "authors"."id" LEFT OUTER JOIN "comments" ON "comments"."author_id" = "authors"."id"
```

If you feel left_outer_joins is too long to type, then Rails 5 also has an alias method left_joins.
