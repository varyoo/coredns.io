+++
title = "alias"
description = "*alias* replaces zone apex CNAMEs."
weight = 10
tags = [  "middleware" , "alias" ]
categories = [ "middleware", "external" ]
date = "2017-07-25T21:57:00+08:00"
repo = "https://github.com/serverwentdown/coredns/middleware/alias"
home = "https://github.com/serverwentdown/coredns/blob/master/middleware/alias/README.md"
+++

The *alias* middleware eliminates CNAME records from zone apex by making the subsequent resolved
records look like they belong to the zone apex. This behaves similarily to [CloudFlare's Zone
Flattening](https://support.cloudflare.com/hc/en-us/articles/200169056-CNAME-Flattening-RFC-compliant-support-for-CNAME-at-the-root).

This middleware only works with the `file` middleware with `upstream` set, or when A or AAAA records
exist alongside the CNAME record.

## Syntax

~~~
alias
~~~

## Examples

```
example.com {
  file example.com.db {
    upstream 8.8.8.8
  }
  alias
}
```

All it does is transform records like this:

```
;; ANSWER SECTION:
example.com.	300	IN	CNAME	some.magic.example.org.
some.magic.example.org. 299 IN A	123.123.45.67
```

into

```
;; ANSWER SECTION:
example.com.	299	IN	A	123.123.45.67
```

## How to Enable

Follow [these](/2017/07/25/compile-time-enabling-or-disabling-middleware/) steps.
