---
layout: post
title: Demandware Open Commerce API Boilerplate
tags: [demandware, open commerce api, open source, backbone.js, node.js]
date: 2012-04-29

section: Blog
---

# Demandware Open Commerce API Boilerplate

[Github Project Link](https://github.com/coderguy/demandware-oc-api-boilerplate)

## Background

So at [work](http://www.fluid.com), I have been working on building e-commerce sites with [Demandware](http://www.demandware.com/).  Demandware is a cool platform.  They have solved a lot of common e-commerce problems well.  They can scale and handle crazy spikes in traffic.  The problem is that up until recently their whole tech stack was a series of proprietary technologies.  I was fortunate to learn them through a week of intense training at Demandware's HQ in the Boston, MA area.  While I was there, I found out that they were working on a set of RESTful APIs that would expose their services in a much friendlier way.  These APIs are called the Demandware Open Commerce APIs.

## Developer Idol

Demandware has an annual conference.  This year's conference includes a programming contest called Developer Idol.  The basic idea it to share work or write something that would help the community as a whole.  I thought I would take my stab at building a single page app storefront.  The APIs currently only have the shop flow (products and categories) exposed.

## The Boilerplate

Boilerplate are all the rage and this is my first time to try to make one.  In the Demandware world, the boiler plate for their tech stack is called Site Genesis.  Ultimately, I hope that my boilerplate becomes a viable alternative to Site Genesis for those wishing to develop with more traditional or modern technologies (node.js, backbone.js, etc).

My goal was to have a product that could be deployed back into the Demandware environment or to a CDN, so that hosting wouldn't be a big issue.  Since the Demandware environment is technologically locked down, I decide to build a single page [backbone.js](http://backbonejs.org) application.  The boilerplate uses [Node.js](http://nodejs.org/) and [grunt.js](http://akdubya.github.com/dustjs/) to build the combined css & js files.  I picked dust.js for the templating.  You can get the full run down of the technologies used over on the [read me](http://github.com/coderguy/demandware-oc-api-boilerplate).

## What's Next

I would like to make the project much more configurable.  Grunt.js can be configured to ask a few questions and output a basic site ready to start customizing.  Additionally, I would also like to keep expanding the boilerplate as new APIs are exposed.

## Conclusion

This is my first open source project.  It is a very humbling feeling putting your code out there for the world to see.  I published it before I thought it was ready to meet the deadline for the contest, but I plan to keep cleaning it up and refining it.