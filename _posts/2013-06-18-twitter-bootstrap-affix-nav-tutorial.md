---
layout: post
title: "Tutorial: Affixed Sidebars with Twitter Bootstrap"
tags: [twitter bootstrap, tutorial]
date: 2013-06-18

section: Blog
---

# Tutorial: Affixed Sidebars with Twitter Bootstrap

So I am trying to use the [affix](http://twitter.github.io/bootstrap/javascript.html#affix) plugin that comes with Twitter Bootstrap.  The affix feature allows you to add a nice fixed sidebar for navigation, that stays in place while you scroll.  It should be a 5 minute setup, but unfortunately this feature seems a bit buggy ([as this 82 comment github issuse shows](https://github.com/twitter/bootstrap/issues/4647)).

## The Steps

### 0. Page setup

Let's assume you have the following setup.

<pre>
&lt;html&gt;
  &lt;head&gt;include bootstrap&lt;/head&gt;
  &lt;body&gt;
    &lt;header&gt;
      &lt;div class=&quot;nav&quot;&gt;&lt;/div&gt;
    &lt;/header&gt;
    &lt;div class=&quot;content&quot;&gt;
      &lt;div class=&quot;row&quot;&gt;
        &lt;div class=&quot;span9&quot;&gt;Great Content Here&lt;/div&gt;
        &lt;div class=&quot;span3&quot;&gt;&lt;div id=&quot;sidebar&quot;&gt;Your article nav&lt;/div&gt;&lt;/span&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/body&gt;
&lt;/html&gt;
</pre>

### 1. Add the data tags

On the element that you want to affix to the navigation you should add the following tags:

```<div id="sidebar" data-spy="affix" data-offset-top="400" data-offset-bottom="200">```

### 2. Setup the styles

The way the plugin works is that it will toggle between one of three classes to the target element:

* .affix-top (when the item is within the offset-top range)
* .affix-bottom (when the item is within the offset-bottom range)
* .affix (when the item is between the top and bottom)


Here are the styles that worked for me:

<pre>
.body {
  position: relative;
}
.affix {
  width: inherit; //helped keep the content the same size on fluid layouts
  position: fixed;
  top: 50px;  //height of the nav
}
.affix-bottom {
  width: inherit;
  position: absolute;
  top: auto;
  bottom: 200px;  //height of the footer
}
.affix-top {
  //i didn't need this style but you might
}
</pre>

A couple of important points.  When you are at the top or bottom of the page, you will rely on absolute positioning.  The affix class in the middle of the page uses fixed position.  Fixed position requires the body have a relative position.

## The Flicker Bug

I followed the documentation and had the sidebar affixed scrolling working very quickly.  The problem I ran into was when the sidebar would get to the bottom it would flicker.  This was due to a number of factors, but the main technical reason was that the plugin was toggling between the affix and affix-bottom classes many times a second.  This bug will probably only manifest itself if you navbar is taller than the viewport minus your header and footer.

### Cause 1

In all of my trial and error, the value I was passing into the offset was 250, but the value in the affix-bottom was 200.  These two values should be the same.

### Cause 2

The body must have the position: relative attribute.

## Conclusion

I hope this write helps you to quickly affix sidebars on your site.