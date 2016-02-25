---
title: Get same time of next week and previous week in rails 5
tip-number: 13
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: We can get the next week or the previous week with the current time using this methods.

---


Support for same_time option to next_week and prev_week

In Rails 4.x next_week returns beginning of next week and prev_week returns beginning of previous week.

In Rails 4.x these two methods also accept week day as a parameter.

```ruby
  Time.current
  => Fri, 12 Feb 2016 08:53:31 UTC +00:00

  Time.current.next_week
  => Mon, 15 Feb 2016 00:00:00 UTC +00:00

  Time.current.next_week(:tuesday)
  => Tue, 16 Feb 2016 00:00:00 UTC +00:00

  Time.current.prev_week(:tuesday)
  => Tue, 02 Feb 2016 00:00:00 UTC +00:00
```

By using week day as parameter we can get the date one week from now but the returned date is still the beginning of that date. How do we get one week from the current time.

Rails 5 add an additional option same_time: true to solve this problem.

Using this option, we can now get next week date from the current time.

```ruby
  Time.current
  => Fri, 12 Feb 2016 09:15:10 UTC +00:00

  Time.current.next_week
  => Mon, 15 Feb 2016 00:00:00 UTC +00:00

  Time.current.next_week(same_time: true)
  => Mon, 15 Feb 2016 09:15:20 UTC +00:00

  Time.current.prev_week
  => Mon, 01 Feb 2016 00:00:00 UTC +00:00

  Time.current.prev_week(same_time: true)
  => Mon, 01 Feb 2016 09:16:50 UTC +00:00
```