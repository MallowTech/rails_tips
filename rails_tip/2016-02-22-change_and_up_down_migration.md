---
title: Migration Change vs Up Down Methods
tip-number: 11
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: We should write migrations with change method if we are not migrating database with manual update, if we are, then we should consider using up down methods and write behaviour that handles the manual update we want.

---

### change

We do not need to write specific down method if we use change method to write migrations

Rails automatically can detect what needs to be reverted considering what was changed in change method

Revert to this type of migrations works only when they are written by Rails Conventions only - like given above using, add_column, remove_column, create_table and so on.

When we try to revert, Rails will not be able to detect manual changes done in change method. e.g. If you alter database with

```ruby
class AddNameToUser < ActiveRecord::Migration

   def change
        add_column :users , :name, :string, :null => false
   end

end
```


### up down methods

We need to define exclusively what should happen when running migration or reverting migration.

Only those changes defined by us in up/down methods will be performed by Rails.

We get more flexibility of defining behaviour for manual updates of database

```ruby
class AddNameColumnToUser < ActiveRecord::Migration 

   def self.up
       add_column :users , :name, :string, :null => false
   end

   def self.down
      remove_column :users , :name, :string, :null => false
   end

end
``` 
