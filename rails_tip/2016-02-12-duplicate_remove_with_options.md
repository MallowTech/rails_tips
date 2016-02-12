---
layout: post

title: Remove duplicate passed to series of method using with_options
tip-number: 01
tip-username: logesh 
tip-username-profile: https://github.com/logeshmallow
tip-description: Removing duplicates out of options passed to a series of methods and avoid more bugs from forgetting to add the necessary options.

---

An elegant way to factor duplication out of options passed to a series of method calls. Each method called in the block, with the block variable as the receiver, will have its options merged with the default options hash provided. Each method called on the block variable must take an options hash as its final argument.

We usually had this dependent called every time and we certainly missed few times unnoticed as shown below

class User < ActiveRecord::Base
  has_many :sample1, class_name: "User", dependent: :destroy
  has_many :sample2, dependent: :destroy
  has_many :sample3, as: :test
end

In the above code we have duplicates and we have also missed dependent in one of our association. So for such scenarios, we can have the with_options used as shown below

class User < ActiveRecord::Base
  with_options dependent: :destroy do |assoc|
    assoc.has_many :sample1, class_name: "User"
    assoc.has_many :sample2
    assoc.has_many :sample3, as: :test
  end
end 


I hope the above tip will be useful.