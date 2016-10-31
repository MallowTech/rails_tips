---
title: Disable model validation on update
tip-number: 30
tip-username: Gokul M
tip-username-profile: https://github.com/mgokul595
tip-description: Updating values in the Database without doing the model validation

---




Generally update_attributes method in rails will validate all fields eventhough it is not being updated.

So, If we need to update the fields without doing such validations we can go with the below two methods:

1. Updating the column one by one using update_attribute:

```ruby
@object.update_attribute(first_name: 'Rails')
```

This will validate & update only the name field and skip validation for other fields. 
Now, Just think what if you need to update more columns. It cause more queries to be executed instead of updating in single query.

2. Updating the column values without any validation:

```ruby
@object.assign_attributes(first_name: 'Ruby', last_name: 'Rails')
@object.save(validate: false)

```

Using above method the validation of the columns can be skipped.

--
