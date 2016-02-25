---
title: Disable multiple time form submit using disable_with attribute
tip-number: 12
tip-username: Logesh
tip-username-profile: https://github.com/logeshmallow
tip-description: Value of this parameter will be used as the value for a disabled version of the submit button when the form is submitted. This feature is provided by the unobtrusive JavaScript driver.

---


To avoid duplicate form submissions, Rails has a nice option for submit tags:

```ruby
submit_tag "Submit", :disable_with => "Saving..."
```

This adds behavior to the submit button to disable it once clicked, and to display "Saving..." instead of "Submit".

### Rails 4+

```ruby
submit_tag 'Submit', data: { disable_with: 'Text' }
```