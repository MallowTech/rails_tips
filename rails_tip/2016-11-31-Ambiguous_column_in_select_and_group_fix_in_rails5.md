---
title: Removing ambiguous column issue in rails 5
tip-number: 31
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: Whenever we have columns with same name in two table and query it, we face ambiguous column issue in select and group by and rails5 fixes it now

---


```ruby
 
    users(:id, :name)
    posts(:id, :title, :user_id)
    comments(:id, :description, :user_id, :post_id)

    >> Post.joins(:comments).group(:user_id).count
    Mysql2::Error: Column 'user_id' in field list is ambiguous: SELECT COUNT(*) AS count_all, user_id AS user_id FROM `posts` INNER JOIN `comments` ON `comments`.`post_id` = `posts`.`id` GROUP BY user_id


    users(:id, :name)
    posts(:id, :title, :user_id)
    comments(:id, :description, :user_id, :post_id)

    >> Post.joins(:comments).group(:user_id).count
    SELECT COUNT(*) AS count_all, "posts"."user_id" AS posts_user_id FROM "posts" INNER JOIN "comments" ON "comments"."post_id" = "posts"."id" GROUP BY "posts"."user_id"

    => { 1 => 1 }

```

This shows that now both projection and Group By are prepended with the posts table name and hence fixing the conflict.
