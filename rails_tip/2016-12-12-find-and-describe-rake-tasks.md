---

title: Find and describe all rake tasks
tip-number: 36
tip-username: prakash 
tip-username-profile: https://github.com/prakash-subramani
tip-description: Find and describe all rake tasks.

---


If you have a large application there is that you’ve written multiple rake tasks. Rails also comes built in with a number of rake tasks that can be hard to remmeber or find. The easiest quickest way to find rake tasks is to run

```bundle exec rake -T 
```

The -T flag tells rake to lists all the rake tasks that it finds in an application. It also prints the description of the task.