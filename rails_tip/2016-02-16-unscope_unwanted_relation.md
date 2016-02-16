---
title: Unscope to remove or modify the unwanted relation
tip-number: 05
tip-username: logesh 
tip-username-profile: https://github.com/logeshmallow
tip-description: We can remove or modify the unwanted relation that is already defined on a chain of relations. This would be useful when modifying relations without reconstructing entire chain.

---

```ruby
User.order(‘email DESC’).unscope(:order) == User.all
```

We can also call this method with multiple arguments as

```ruby
User.order(‘email DESC’).select(‘id’).unscope(:order, :select) == User.all
```

Also, we can unscope :where values like

```ruby
User.where(name: “mallow”, active: true).unscope(where: :name) == User.where(active: true)
```

We can use in association definition

```ruby
has_many :posts, -> { unscope where: :removed }
```

I hope the above tip will be useful.
