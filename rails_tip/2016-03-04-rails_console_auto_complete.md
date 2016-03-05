---
title: Rails console autocomplete to save time 
tip-number: 21
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: In rails, we use rails console to test and interact directly with models and such from the command line and when we do so we can use the below set of tips to improve efficiency.

---

Rails console has autocompletion support, which I think would definitely save lot of time instead of typing in the commands everytime.

Suppose you have a Picture model that you previously used in the console and now you want to use it to run a query. Start by typing Mov and then hit Tab:

```ruby
>> Pic<Tab>
```

There's only one possible completion in this case, so it's autocompleted to what you want:

```ruby
>> Picture
```

Given the class, you now want to use the where method to run the query. Start by typing .w and then hit Tab:

```ruby
>> Picture.w<Tab>
```

There's more than one valid completion in this case, so nothing happens (you may hear a bell). Now hit Tab a second time and you'll get a list of valid completions:

```ruby
>> Picture.w<Tab><Tab>

Picture.where                 
Picture.with_scope
Picture.with_exclusive_scope
Picture.with_warnings
Picture.with_options
```

You want the where method, so type the next character in the method name (h) and hit Tab yet again:

```ruby
>> Picture.wh<Tab>
```

Bingo. That narrows it down to only one possible completion, so it's expanded to what you want:

```ruby
>> Picture.where
```

Autocompletion saves a lot of typing and remembering. When in doubt, just keep hitting the Tab key. It will autocomplete class names, method names, and any variable/object names within the scope of the console session.

Getting the Value of the Last Expression
I can't begin to tell you how many times this one has come in handy. Here's an all-too-familiar situation: I manage to correctly type a useful hunk of code into the console, such as this query:

```ruby
>> Picture.where("total_likes >= ?", 1000).order(:name)
```

I immediately hit Enter and the query runs. Then I remember that I actually wanted to do something with the results, but failed to assign the results to a variable. At this point I could hit the up arrow key to recall that line of code and then edit it, but there's an easier way.

The return value of the last expression is automatically stored in the special underscore (_) variable. To assign the query results to a pictures variable, for example, I can use:

```ruby
>> pictures = _
```

Then I can actually do something with the results, such as counting the number of pictures:

```ruby
>> pictures.size
=> 5
```

Alternatively, I could have called the size method directly on the _ variable:

```ruby
>> _.size
=> 5
```

It's important to keep in mind that _ always contains the value of the last expression. So at this point the value of _ has changed to be the result of calling size on the array of pictures:

```ruby
>> _
=> 5
```

Neat little trick, that one.
