---
layout: post
title: "The curious case of localhost"
date: 2017-09-12 20:05:54 +0430
tags: [openbsd,libc,ping,isc,bind,ping,gethostbyname,ipv4,resolv.conf,host]
---

The desktop is ready and the packages are installed and now it's time to see
 how its PHP package is built. Wanted to see it in browser so I run the:

```sh
$ php-7.0 -S localhost:8000
```

And frozen.. Thought it might be some security restriction that doesn't let
 the PHP process to listen on a TCP port. But it was not!

So, let us run it on `127.0.0.1:8000`. Oops, it's working.. But why?

After some investigation, I've found something really interesting.

The `ping` utility could not ping(**resolve**, to be specific) the `localhost`
 but when I type the `$ host localhost` it shows the `127.0.0.1`.

Something is so weird here. How come that `ping(8)` and `host(1)` are **NOT**
 using the same resolve(r) function in their code?

After some investigation, I found that they're coming from totally different
 planets and have nothing in common!

Of course I could "get rid of" this problem by adding the `lookup` directive to
 the `/etc/resolv.conf` but where is the fun in doing so?

To be updated perhaps.
