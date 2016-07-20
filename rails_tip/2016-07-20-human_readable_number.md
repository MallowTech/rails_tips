---
title: Convert a number into human readable
tip-number: 29
tip-username: Jayaprakash
tip-username-profile: https://github.com/JPMallow
tip-description: To convert the number into human readable format, you can use number_to_human helper method in Rails - http://api.rubyonrails.org/classes/ActionView/Helpers/NumberHelper.html

---

To convert the integer numbers into human readable format.

```ruby
number_to_human(123)                                          # => "123"
number_to_human(1234)                                         # => "1.23 Thousand"
number_to_human(12345)                                        # => "12.3 Thousand"
number_to_human(1234567)                                      # => "1.23 Million"
number_to_human(1234567890)                                   # => "1.23 Billion"
number_to_human(1234567890123)                                # => "1.23 Trillion"
number_to_human(1234567890123456)                             # => "1.23 Quadrillion"
number_to_human(1234567890123456789)                          # => "1230 Quadrillion"
number_to_human(489939, precision: 2)                         # => "490 Thousand"
number_to_human(489939, precision: 4)                         # => "489.9 Thousand"
number_to_human(1234567, precision: 4,
                        significant: false)                   # => "1.2346 Million"
number_to_human(1234567, precision: 1,
                        separator: ',',
                        significant: false)                   # => "1,2 Million"

number_to_human(500000000, precision: 5)                      # => "500 Million"
number_to_human(12345012345, significant: false)              # => "12.345 Billion"
```

Non-significant zeros after the decimal separator are stripped out by default (set :strip_insignificant_zeros to false to change that):

```ruby
number_to_human(12.0000) # => “12” 
number_to_human(12.0000, precision: 4, strip_insignificant_zeros: false) # => “12.00”
```

### Troubleshooting

If you receive the following error 

```
NoMethodError: undefined method `number_to_human' for main:Object
```

include NumberHelper in your controller / views.

```ruby
include ActionView::Helpers::NumberHelper
```
