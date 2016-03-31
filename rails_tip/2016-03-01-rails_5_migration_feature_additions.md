---
title: rails 5 migration feature additions
tip-number: 19
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: Rails 5 has changed migration API where not null is automatically added for timestamps and sets index for reference columns

---

In Rails 4.x command

rails g model User name:string

will generate migration as shown below.

```ruby
class CreatePosts < ActiveRecord::Migration[5.0]
  def change
    create_table :posts do |t|
      t.string :title

      t.timestamps null: false
    end
  end
end
```

In Rails 5 the same command will generate following migration.

```ruby
class CreatePosts < ActiveRecord::Migration[5.0]
  def change
    create_table :posts do |t|
      t.string :title

      t.timestamps
    end
  end
end
```

But the schema generated after running migration in rails 5 would be

```ruby
sqlite> .schema posts
CREATE TABLE "posts" ("id" INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL, "title" varchar, "created_at" datetime NOT NULL, "updated_at" datetime NOT NULL);
sqlite>
```

In Rails 4.x command

rails g model Task user:references

would generate following migration.

```ruby
class CreateTasks < ActiveRecord::Migration
  def change
    create_table :tasks do |t|
      t.references :user, index: true, foreign_key: true
      t.timestamps null: false
    end
  end
end
```

In Rails 5.0, same command will generate following migration.

```ruby
class CreateTasks < ActiveRecord::Migration[5.0]
  def change
    create_table :tasks do |t|
      t.references :user, foreign_key: true

      t.timestamps
    end
  end
end
```

There is no mention of index: true in the above migration. Let’s see the generated schema after running Rails 5 migration.

```ruby
sqlite> .schema tasks
CREATE TABLE "tasks" ("id" INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL, "user_id" integer, "created_at" datetime NOT NULL, "updated_at" datetime NOT NULL);

CREATE INDEX "index_tasks_on_user_id" ON "tasks" ("user_id");
```

If we look closer at the migrations of rails 5, you could see class is now inheriting from ActiveRecord::Migration[5.0] instead of ActiveRecord::Migration and this indicates the migration is created from rails 5