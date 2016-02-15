---
title: Formatting numbers to different representation
tip-number: 04
tip-username: logesh 
tip-username-profile: https://github.com/logeshmallow
tip-description: We represent numbers in different format and this could be done easily using number of ways listed below.  

---

Below are list of representations

1) Telephone numbers
2) Currency 
3) Percentage
4) Delimited
5) Rounded
6) Human size
7) Human

## Telephone number
```ruby
1235551234.to_s(:phone, country_code: 1)  # => +1-123-555-1234
```

## Currency
```ruby
1234567890.506.to_s(:currency, precision: 3)  # => $1,234,567,890.506
```

## Percentage
```ruby
1000.to_s(:percentage, delimiter: '.', separator: ',')  # => 1.000,000%
```

## Currency
```ruby
1234567890.506.to_s(:currency, precision: 3)  # => $1,234,567,890.506
```

## Delimited
```ruby
12345678.to_s(:delimited, delimiter: ",")  # => 12,345,678
```

## Rounded
```ruby
111.2345.to_s(:rounded, significant: true)  # => 111
```

## Human size
```ruby
1234567.to_s(:human_size)  # => 1.18 MB
```

## Human
```ruby
12345.to_s(:human)  # => "12.3 Thousand"
```

I hope the above tip will be useful.
