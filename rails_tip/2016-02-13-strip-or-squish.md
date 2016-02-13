---
title: Where use strip or squish 
tip-number: 02
tip-username: logesh 
tip-username-profile: https://github.com/logeshmallow
tip-description: Removing leading or trailing spaces can be done using both methods but squish also substitutes single space with multiple spaces in between string.

---

We use strip to remove leading and trailing spaces. But some times, we require removing spaces between strings or substitute mistakenly typed two or more spaces with one space and for that case, we can use squish.

##strip:

Returns a copy of str with leading and trailing whitespace removed

```ruby
"    mallow    ".strip   #=> "mallow"
"\trails dev\r\n".strip   #=> "rails dev"
" foo bar ".strip #=> 0.005ms
```

##squish:

Returns the string, first removing all whitespace on both ends of the string, and then changing remaining consecutive whitespace groups into one space each.

```ruby
%{ Multi-line
   string }.squish                   # => "Multi-line string"
" foo   bar    \n   \t   boo".squish # => "foo bar boo"
" foo bar ".squish #=> 0.029ms
```

I hope the above tip will be useful.
