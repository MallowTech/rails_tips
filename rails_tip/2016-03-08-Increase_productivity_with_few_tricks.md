---
title: Increase productivity with few tricks
tip-number: 26
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: We often do some repetitive things that won’t seem like taking much time but it actually does and the following are some of the tricks that would reduce some time of that kind.

---

### Quickly search command line history

When you use large commands with multiple arguments from terminal, it would be difficult to remember that. And we might google it again and instead we can make use of *Ctrl + r*

Open your terminal and press *Ctrl + r*. Start typing the first few chars of the command that you recently used. It should start showing you commands that matches your command query. If there is more than one command that matches, press *Ctrl + r* repeatedly to cycle through the commands that match your query. Press *Ctrl + e* to select a particular option.

You can also say *history* in the command line to a list of every command that you may have executed.

### Reduce backspace time

When typing a really long command line piece that spans 4 lines. Only to realise that you made a mistake in the beginning of the line? Now if you don’t know the shortcuts, you would probably press the right arrow to go to the beginning of the line character by character. But the pros know better. They use shortcuts. These shortcuts will save you hours of time playing with the arrow and backspace keys.

*Ctrl + k* - Deletes everything to the right of the cursor

*Ctrl + w* - Deletes everything to the left of the cursor (one word at a time)

*Ctrl + a* - Go to the beginning of the line

*Ctrl + e* - Go to the end of the line


### Reload the console on the fly

You try something in the console, it doesn’t work. You change your code and try again? Nope got to restart the console session first. Sure its fine in the beginning but it starts to be a drag after a while. You can avoid this problem most of the time by simply saying

```ruby
reload!
```

It will reload your entire Rails application without you having to terminate the session.

