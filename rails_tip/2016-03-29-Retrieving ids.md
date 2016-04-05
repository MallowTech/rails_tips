---
title: Retriving the ids of the has_many or has_many_through relationships
tip-number: 29
tip-username: Bala Karthik
tip-username-profile: https://github.com/balakarthik2011
tip-description: Retriving the ids of the has_many or has_many_through relationships

---




For example if You have two models post and comments
 
 post has many comments
 
 comments belongs to post
 
 if you want to retrive the ids of the comment of a particular post.
 
 you can use,

```ruby
 
 comments = Post.find(id).comment_ids
```

This is efficient when compared to using functions like map,pluck.


```ruby
 >> Post.first.comments.map(&:id)
   Post Load (1.0ms)  SELECT  "posts".* FROM "posts"  ORDER BY "posts"."id" ASC LIMIT 1
   Comment Load (3.0ms)  SELECT "comments".* FROM "comments" WHERE "comments"."post_id" = $1  [["post_id", 1]]
 [1,4,6]
```


```ruby
 >> Post.first.comments.pluck(:id)
   Post Load (1.5ms)  SELECT  "posts".* FROM "posts"  ORDER BY "posts"."id" ASC LIMIT 1
    (1.2ms)  SELECT "comments"."id" FROM "comments" WHERE "comments"."post_id" = $1  [["post_id", 1]]
 [1,4,6]

```


```ruby
 Post.first.comment_ids
   Post Load (1.0ms)  SELECT  "posts".* FROM "posts"  ORDER BY "posts"."id" ASC LIMIT 1
    (1.0ms)  SELECT "comments".id FROM "comments" WHERE "comments"."post_id" = $1  [["post_id", 1]]
 [1,4,6]
```

