---
title: Rendering views outside of controllers in Rails 5
tip-number: 14
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: Sometimes we want to render our HTML or JSON response outside of this request-response cycle and there we can use this option.

---


Rails 5 has this feature baked in.

Let’s say we have a OrdersController and we want to render individual order outside of controller.

Fire up rails console and execute following command.

```ruby
OrdersController.render :show, assigns: { order: Order.last }
```

This will render app/views/orders/show.html.erb with @order set to Order.last. Instance variables can be set using assigning the same way we use them in controller actions. Those instance variables will be passed to the view that is going to be rendered.

Rendering partials is also possible.

```ruby
OrdersController.render :_form, locals: { order: Order.last }
```

This will render app/views/orders/_form.html.erb and will pass order as local variable.

Say I want to render all orders, but in JSON format.

```ruby
OrdersController.render json: Order.all
# => "[{"id":1, "name":"The Well-Grounded Rubyist", "author":"David A. Black"},
       {"id":2, "name":"Remote: Office not required", "author":"David & Jason"}]
```

Even rendering simple text is possible.

```ruby
>> BooksController.render plain: 'this is awesome!'
  Rendered text template (0.0ms)
# => "this is awesome!"
```

Similar to text, we can also use render file and render template.

