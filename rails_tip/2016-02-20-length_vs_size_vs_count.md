---
title: length vs size vs count
tip-number: 09
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: These are similar ones which can be used in Arrays, Hashes or Objects. So where to use these and why is what is covered here.

---

### length

Basically length method used on arrays in ruby returns number of elements in the array for which method is invoked.

Example, suppose we have array a as,

```ruby
a = [1,2,3,4,5,6,7]
a.length
=> 7
```

### size

Size is just an alias to the Array#length method. It executes same Array#length method internally.

Example,

```ruby
b = [1,2,3,4]
b.size
=> 4
```

### count

Count has some more functionalities than length/size. It can be used for getting number of elements based on some condition. 

Example:

Suppose we have array c as,

```ruby
c = [1,2,3,4,4,7,7,7,9]
c.count
=> 9

c.count 7
=> 3

c.count {|i| i>5}
=> 4
```

Array#count should be used only for getting number of elements in array based on some condition.

Otherwise, for getting number of elements without any condition use Array#length or Array#size.