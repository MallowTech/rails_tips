---
title: Rails 5 parameter filter improvement 
tip-number: 24
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: Rails makes it very easy to filter data like passwords, credit card information, auth keys etc and  prevent it from appearing in log files for security reason.

---

By adding following line in application.rb, we can filter senstive information.

```ruby
config.filter_parameters += [:password]
```

Now the log file will show [FILTERED] instead of real password value.

This replacement of password with [FILTERED] is done recursively.

```ruby
{user_name: "john", password: "123"}
{user: {name: "john", password: "123"}}
{user: {auth: {id: "john", password: "123"}}}
```

In all the above cases, “123” would be replaced by “[FILTERED]”.

Now think of a situation where we do not want to filter all the occurrence of a key. 

Here is an example.

```ruby
{credit_card: {number: "123456789", code: "999"}}
{user_preference: {color: {name: "Grey", code: "999999"}}}
```

We definitely want to filter [:credit_card][:code] but we want [:color][:code] to show up in the log file.

This can be achieved in Rails 5.

The application.rb changes from

```ruby
config.filter_parameters += ["code"]
```
to
```ruby
config.filter_parameters += ["credit_card.code"]
```

In this case so long as parent of code is credit_card Rails will filter the data.

