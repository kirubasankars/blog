---
title: "Check JavaScript disabled in the browser Check JavaScript disabled in the browser"
date: 2013-08-21T17:51:28-04:00
draft: false
tags: ["browser", "javascript", "website"]
thumbnail: "ass"
---

For security concern, user may like to disable JavaScript in their web browser. If it is, raise a big problem in many website which depends on JavaScript to function well.

The problem is, there is no http request header from browser to identify is javascript enabled/disabled to process subsequent http request process for nojavascript browsers. You can use following methods to do so.

You can do get request to notify server to say JavaScript is disabled only when it is disabled. Is it sounds good? Using img tag.
Example below.

This get request will only triggered when no JavaScript is enabled. You can use some unique id to identify users has javascript disabled.

```
<noscript>
  <img src=”nojavascript.[asp/aspx/php/jsp]?userid=[userid]” />
</noscript>
```


