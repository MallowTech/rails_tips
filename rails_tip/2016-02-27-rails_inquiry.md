---
title: Inquiry in rails
tip-number: 16
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: The inquiry method provides friendlier way to check both string and array using the StringInquirer and ArrayInquirer

---

The inquiry method converts a string into a StringInquirer object making equality checks prettier.

```ruby
"production".inquiry.production? # => true
"active".inquiry.inactive?       # => false
```

Array#inquiry is a shortcut for wrapping the receiving array in an ArrayInquirer

```ruby
  users = [:mark, :max, :david]

  array_inquirer1 = ActiveSupport::ArrayInquirer.new(users)

  # creates ArrayInquirer object which is same as array_inquirer1 above
  array_inquirer2 = users.inquiry

  array_inquirer2.class
  => ActiveSupport::ArrayInquirer

  # provides methods like:

  array_inquirer2.mark?
  => true

  array_inquirer2.john?
  => false

  array_inquirer2.any?(:john, :mark)
  => true

  array_inquirer2.any?(:mark, :david)
  => true

  array_inquirer2.any?(:john, :louis)
  => false
```