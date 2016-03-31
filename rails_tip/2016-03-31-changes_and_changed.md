---
title: Get same time of next week and previous week in rails 5
tip-number: 13
tip-username: Surender
tip-username-profile: https://github.com/harrysuren
tip-description: We can check the status of an ```ActiveRecord``` Object and its variables by using these methods.

---


ActiveRecord keeps a sizable amount of information about an object while it undergoes updates. A hash, accessible via the changes method, acts a central location for these updates.

**```changes```**

Each key in the changes hash maps to a record’s attribute. The value of each key is an Array with two elements: what the attribute value used to be, and what it is now:

```ruby
  order = Order.find(1)
  order.user_id
  # => 10
  order.user_id = 11
  order.changes
  # => {"user_id"=>[10, 11]}
```

**a. ```changed?```**

A simple boolean method changed? is available to determine if anything on the object is different since its retrieval.

```ruby
  order = Order.find(1)
  order.user_id = 11
  order.changed?
  # => true
```

However, if the same value is set on a model, regardless of the value’s object_id, changed? returns false:

```ruby
  order = Order.find(1)
  order.user_id
  # => 1
  order.user_id = 1
  order.changed?
  # => false
```

Two “different” strings were set to book.title but since they resolve to the same characters, the object is not changed?.

When using PostgreSQL, the ```changed?``` method can save unnecessary ```begin``` and ```commit``` transaction calls for objects that have no changes:

```ruby
  class OrdersController < ApplicationController
    def update
      @order = Order.find(order_params[:id])
      @order.assign_attributes(order_params)
      @order.save! if @order.changed?
    end
  end
```

**b. ```<attribute>_was```**

Accessing the same ```changes``` hash as the ```changed?``` method, ```<attribute>_was``` returns the value of an attribute before it was reassigned:

```ruby
  order = Order.find(1)
  order.status
  # => 'waiting'
  order.status = 'delivered'
  # => 'delivered'
  review.status_was
  # => 'waiting'
```