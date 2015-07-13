---
layout: post
title: "Owning Rails Course Notes"
tags:
- ruby
---

A while ago I attending the [http://owningrails.com](Owning Rails course). It was a fantastic course which de-mystified Rails by showing it's not magic - it just sometimes uses Rubys syntax to hide how it works.

This is a bit of a brain-dump of what I learnt - but you should go on the course, well worth the money.

## Ruby Method Syntactic Sugar

Because Ruby method calls will be called on `self` by default and brackets are not manditory, this means that the below statements are equivalent:

```ruby
before_filter :authenticate! ≡ HomeController.before_filter(:authenticate!)
```

## Modules vs Classes

* `extend` adds module functions at class level
* `include` add module functions at instance level
* `@attribute` is instance level variable, includes in this instance only
* `@@attribute` is a class level variable, included in subclasses

Put methods in `ClassMethods` module to put them on the parent class, not the current module.

If you need to call `super` in a module method, you need to subclass the parent so that methods aren't overridden. By default, ruby will execute the _first_ match.

`binding` is a private method for the class containing instance variables etc.

`autoload :constant` lazy-loads the module so may save memory.

## Blocks and Lambdas

* Blocks are not objects, `Procs` are
* Lambdas checks the number of arguments when called. Lambdas don't
* Everything is an object (except blocks...)
* `yield` calls blocks. Same as `&block` argument. Converts block to `Proc`
* `yield` executes codes in root context. `&block` executes in that instance using `instance_eval`
* `&block` converts block to a `Proc`. `instance_eval` takes `Proc`/`String` not a block
* `&method(:name)` converts method to block

## Rack

Rack is a protocol, it defines how a webserver talks to Rails and how Rails talks to the webserver

## Conventions

Use `_` to ingore that variable, i.e.

```ruby
_, name = 'boring/important'.split('/')
```
