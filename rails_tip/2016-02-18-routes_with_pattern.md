---
title: Pattern matching on Routes
tip-number: 06
tip-username: Surender Thillainathan
tip-username-profile: https://github.com/harrysuren
tip-description: Getting teh desired routes which matches the given pattern/string

---

### Rails 4 and below

`rake routes` will give us the available routes in a Project.

If we need to get only some routes which all are related to the User.
 
Its will gives us the routes which are matches to the pattern 'user'
  
```ruby
$ rake routes | grep user
                        new_user_session GET    /login(.:format)                                              devise/sessions#new
                            user_session POST   /login(.:format)                                              devise/sessions#create
                    destroy_user_session DELETE /sign_out(.:format)                                           devise/sessions#destroy
                           user_password POST   /reset(.:format)                                              devise/passwords#create
                       new_user_password GET    /reset/new(.:format)                                          devise/passwords#new
                      edit_user_password GET    /reset/edit(.:format)                                         devise/passwords#edit
```

### Rails 5

We can use both `rake routes` and `rails routes` to get all the available routes for a Project


`Rails 5` added some options to routes

To get Controller specific routes we can use the option `-c`

```ruby
# Controller name
$ rake routes -c users
                                all_users GET    /users(.:format)                                              users#index
                                 new_user GET    /users/new(.:format)                                          users#new
                              create_user POST   /additional_users(.:format)                                   users#create
                              update_user PATCH  /additional_users/:id(.:format)                               users#update
                                edit_user GET    /users/:id/edit(.:format)                                     users#edit

```


```ruby
# Namespaced Controller
$ rake routes -c admin/users
                                all_users GET    /users(.:format)                                              users#index
                                 new_user GET    /users/new(.:format)                                          users#new
                              create_user POST   /additional_users(.:format)                                   users#create
                              update_user PATCH  /additional_users/:id(.:format)                               users#update
                                edit_user GET    /users/:id/edit(.:format)                                     users#edit

```


```ruby
# Namespaced Controller
$ rake routes -c Admin::UsersController
                                all_users GET    /users(.:format)                                              users#index
                                 new_user GET    /users/new(.:format)                                          users#new
                              create_user POST   /additional_users(.:format)                                   users#create
                              update_user PATCH  /additional_users/:id(.:format)                               users#update
                                edit_user GET    /users/:id/edit(.:format)                                     users#edit

```


To get teh Pattern matched routes like `grep` we can use the option `-g'


```ruby
# Search with HTTP verb
$ rake routes -g GET
                                all_users GET    /users(.:format)                                              users#index
                                 new_user GET    /users/new(.:format)                                          users#new
                                edit_user GET    /users/:id/edit(.:format)                                     users#edit
```


```ruby
# Search with pattern
$ rake routes -g password
                                     user_password POST   /reset(.:format)                                              devise/passwords#create
                                 new_user_password GET    /reset/new(.:format)                                          devise/passwords#new
                                edit_user_password GET    /reset/edit(.:format)                                         devise/passwords#edit
```