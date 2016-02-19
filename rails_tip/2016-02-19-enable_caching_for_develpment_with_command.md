---
title: Enabling caching for development without restarting the app.
tip-number: 08
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: Enable caching in development mode without restarting the app using the command

---

### Rails 4

In rails4 we need to turn caching “on” by opening file config/environments/development.rb and changing following line.

```ruby
config.action_controller.perform_caching = false
```

After changing the value from false to true, I need to restart the server.

This means that if I am testing caching behavior locally then every time I turn caching “on” or “off” I need to restart the server.


### Rails 5  

Rails 5 has introduced a new command to create development cache and help us test how caching behaves in development mode. Here is the issue and here is the pull request.

```ruby
$ rails dev:cache
Development mode is now being cached.
```
Execution of the above command creates file caching-dev.txt in tmp directory.

Advantage:

The advantage is that we do not need to restart the server manually if we want to turn caching “on” or “off”. It is internally taken care by the dev_cache method that is executed when rails dev:cache is executed. 

Please note that this feature is not supported by unicorn, thin and webrick. 

Disabling development cache:

Execute the same command that was used to enable caching. If caching was previously enabled then it will be turned “off” now.

```ruby
$ rails dev:cache
Development mode is no longer being cached.
```