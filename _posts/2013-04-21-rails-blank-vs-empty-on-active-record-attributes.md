---
layout: post
title: "Quick Tip: Blank vs Empty on an ActiveRecord Attribute"
tags: [rails, activerecord, quick tip]
date: 2013-04-21

section: Blog
---

{% include quick-tip.html %}

# Quick Tip

I wanted to check to see if an attribute on my ActiveRecord module was empty.

## empty?

When I tried this:

<pre>
s = Subscription.find(1)
if(s.instagram_username.empty?)
  # do something
end
</pre>

I was getting:

```
NoMethodError: undefined method `empty?' for nil:NilClass
```

## blank?

I did a little poking around and fired up my rails console.

<pre>
$ rails c
1.9.3p392 :01 > s.instagram_username
 => nil
1.9.3p392 :02 > nil.empty?
NoMethodError: undefined method `empty?' for nil:NilClass
1.9.3p392 :03 > nil.blank?
 => true
1.9.3p392 :03 > s.instagram_username.blank?
 => true
</pre>

I found out that my attribute was nil, so the empty method wasn't defined on it.

Rails has a nice solution the [blank?](http://api.rubyonrails.org/classes/Object.html#method-i-blank-3F) method.  blank? means that `An object is blank if it’s false, empty, or a whitespace string. For example, “”, “ ”, nil, [], and {} are all blank.`