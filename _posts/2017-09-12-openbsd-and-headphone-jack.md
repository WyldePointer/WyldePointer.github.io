---
layout: post
title: "OpenBSD and Headphone Jack"
date: 2017-09-12 19:23:15 +0430
tags: [openbsd,mixerctl,audio,music,output,headphone,speaker,jack,mute,rtfm]
---

The built-in speakers of this laptop was working perfectly and when I tried
 to connect the external speakers to its headphone jack, there was a big
 silence in the room.

After the `RTFM`, I've found the following command:

```sh
$ mixerctl -av
```

Which has displayed a very interesting variable:

```
outputs.hp.mute=on
```

Hmm, so that one mutes the "HP" output somehow, suggests the name. Let me see
 if I can get the magic smoke out of this ~12 years old laptop:

```sh
$ mixerctl outputs.hp.mute=off
```

That's it, now it's working but I think(read, **believe**) it's just
 temporary and if I restart(or even logout?) it will disappear. Later I'll
 update this post and share the result of writing this variable into the
 `/etc/mixerctl.conf`.

### Update
It's working like a charm. No need to run `mixerctl` after each and every
 reboot.
