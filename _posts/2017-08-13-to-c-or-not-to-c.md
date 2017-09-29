---
layout: post
title: "To C or not to C."
category: c-language-tutorials
date: 2017-08-13 01:07:17 +0430
tags: [programming,unix,language,c,compile,compiling,terminal]
---

01 Is that a question, really?

I've seen that many people are suggesting many languages as the first
 programming language to learn. Personally, I feel like without knowing the
 data and data structure, you're not going to be good at any programming
 language. (As a friend of mine calling some painters "painting-er"(literal
 translation of "Naqqashi-kesh" in Persian), you're going to be a "code-inger",
 not a programmer.)

First of all, everything is number. ANYTHING! (In UNIX philosophy though,
 everything is file. *phew*)

We humans, are using `base-10` or `decimal` numbering systems. Why? Count your
 fingers and you'll get the answer. (Later on, you will need to have your own
 "totem" as well ;)

Computers on the other hand, are using base-2 or binary system, which is, as
 you can guess, 0 and 1.

(If you want to know more about these stuff, I highly recommend you to watch
 <a href="https://www.youtube.com/watch?v=tpIctyqH29Q" target="_blank">Crash
 Course - Computer Science</a>)

The good news is, for writing some codes in C, you don't need to talk in Latin
 or drinking diesel fuel. Knowing the base-10 itself is enough for the
 beginning.

`C` is actually a high-level programming language[1] and it's much closer to
 human languages[2] than it is to the machine-language. (We would call it
 `assembler` then, and not `C`.)

In order to "run" the codes that you write in `C`, you must `compile` them
 first, so they'll be understandable for the computer. (or "The machine". Feel
 free to play "Pink Floyd - Welcome to the Machine" during this tutorial.)

If you're using *NIX systems(including GNU/Linux distributions or BSD family
 including MAC OS) you already have the C compiler in your base system and
 there is no need for any extra packages to be installed.

If you're using Microsoft Windows however, the "Express"(free, as in beer)
 version of Microsoft Visual Studio(any version) would do the job.

The first code that you're going to write is the cool old "hello, world!" and
 before we begin, promise me to not ask "WTF is `argc` and `argv`?" or
 "studio"! Later on you'll master them but for now, just accept it the way that
 you've accepted the color of "blue" or the concept of "empty". (They're what
 they are, just ignore them for now.)

```c_cpp
#include <stdio.h>

int main(int argc, char *argv[]){

  printf("hello, world!\n");

  return 0;
}
```

Save this 8 lines of code as `hello.c` in your `/tmp/` directory (or %tmp% in
 Microsoft Windows) and order your compiler(like a boss! B-) to make it
 "machine-readable":

```sh
$ cc -o /tmp/hello /tmp/hello.c
```

Nothing has happened, huh? Well, UNIX is a "do more and talk less"[3] being and
 whenever it runs something successfully, it won't notify the whole world about
 what it has done. (Unless you ask for it, that's where the `-v` or `--verbose`
 comes into the game.)

So, if nothing has appeared on your screen and now you're on the next line of
 your shell(or "terminal"), it means that your code is compiled and there was
 nothing wrong during the different stages of compilation. (Yeah, there are a
 lot more going on "under the hood".)

Let's run your first program(or application) and see what it will do:
```sh
$ /tmp/hello 
hello, world!
```

Oh, awesome! you just kicked some *cough*!

If you're looking for the next post, then you're ready to learn it, and if not,
 `GOTO 01` and read this post again.(and again)

[1] No, puleaseee! no more "mid" vs "low" vs "high" talk!

[2] English to be specific, since it has been made in United States first.

[3] Or "Talk less but talk wiser".
