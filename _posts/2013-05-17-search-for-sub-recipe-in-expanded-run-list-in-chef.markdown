---
layout: post
title: Search for Sub-Recipe in Expanded Run List in Chef
tags:
- ruby
---
If you are wanting to search for all nodes with a recipe in Chef you can [search](http://docs.chef.io/chef_search.html#nodes):

```ruby
search(:node, 'recipes:ruby-build')
``` 

If you want to search for a sub-recipe (instead of ruby_build::default), you need to double escape it, like: 

```ruby
search(:node, 'recipes:glusterfs\\:\\:server')
```

This took me **ages** to figure out and there doesn't seem to be any documentation written about it.
