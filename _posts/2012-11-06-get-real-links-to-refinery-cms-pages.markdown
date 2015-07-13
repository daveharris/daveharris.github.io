---
layout: post
title: Get real links to Refinery CMS pages
tags:
- Ruby
---
Getting a link to a Refinery CMS Page is harder than you think. To get it to produce the link including parent paths etc use:

```ruby
refinery.url_for(@page.url_marketable)
```

This will return something like:

```
/about-this-site/terms-of-use
```

Easy right?! There doesn't seem to be any documentation about this, you are just meant to know.
