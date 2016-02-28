---
title: Custom queue name for mailer
tip-number: 17
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: We can customise the queue name of the mailer rather than to have the default name that is assigned.

---

In Rails 4.2, Active Job was integrated with Action Mailer to send emails asynchronously.

Rails provides deliver_later method to enqueue mailer jobs.

All outgoing mails are given the queue named “mailers” and we do not have the option of changing this queue name from “mailers” to anything else.

In Rails 5, we can now change queue name for mailer jobs using following configuration.

```ruby
config.action_mailer.deliver_later_queue_name = 'testqueue'
```

```ruby
class TestMailer < ApplicationMailer
  def send_msg(dev)
    @developer = dev
    mail(to: dev.email)
  end
end

2.2.3 :004 > dev = Developer.first
=> <User id: 1, name: “Logesh”, email: “logesh@mallow-tech.com”>

2.2.3 :005 > TestMailer.send_msg(dev).deliver_later
=> <ActionMailer::DeliveryJob:0x008gfb3224d2e0 @arguments=[“TestMailer", "send_msg”, "deliver_now", <User id: 1, name: “Logesh”, email: “logesh@mallow-tech.com”>], @job_id=“876543r3-456e-3b1c-9264-9876tr54re32”, @queue_name="testqueue", @priority=nil>
```



