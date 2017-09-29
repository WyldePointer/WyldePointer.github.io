---
layout: post
title: "The numbers"
category: c-language-tutorials
date: 2017-08-13 06:59:11 +0430
tags: [programming,unix,language,c,compile,compiling,terminal,decimal,short,int]
---

A number is a number, or to be specific, a digit. This digit(s) can be
 represented in many different ways and in most cases, you're going to
 represent them in base-10(decimal) or base-16(hexadecimal, or simply, `hex`).

In order to "print"[1] a decimal number(remember, decimal is base-10 or
 "human-readable number") we use the `%d` specifier with `printf()` function,
 which means, "Whenever you've reached this %d, replace it with a decimal
 number from the arguments that I've passed to you.", and no worries if you
 didn't understand what I just said. Let's write it done. (`GOTO 02`)

```c_cpp
#include <stdio.h>

int main(int argc, char *argv[]){

  printf("My number is %d.\n", 65);

  return 0;
}
```

Compile and run:
```sh
$ cc -o /tmp/numbers.bin /tmp/numbers.c
$ /tmp/numbers.bin
My number is 65
```

What if I told you, this very number here(or there) can be represented as
 a(n alphabet) letter! Or to make it more complicated, telling you that almost
 all "string"s are made of nothing but numbers![2]

Let's have a look at how C is handling various type of data:

 - char: A character, or the smallest data type, which is 1 byte.
 - short: Bigger than a char and must be "at least" 2 bytes.
 - int: Basic integer, bigger than short and "at least" 2 bytes.
 - long: Bigger than int and "at least" 4 bytes. (Finally! 32-bits! Yes! that
 is *exactly* related to your operating system and CPU architecture!)

Think of the data type as "size of a box" which you put your stuff in it.

Numbers can be either signed or unsigned, and by default, when you declare or
 define your variables, they will be in *signed* form, which means, they can
 hold either a negative *OR* a positive value. Let's have a look on the
 supported range of each one: (On a typical x86 machine, of course!)

 - char: -127 to +127
 - unsigned char: 0 to +255
 - short: −32,767 to +32,767
 - unsigned short: 0 to +65535
 - int: −32,767 to +32,767
 - unsigned int: 0 to +65535 (Yeah, WTF!)
 - long: −2,147,483,647 to +2,147,483,647
 - unsigned long: 0 to 4,294,967,295

If you're confused about some of these values, repeat with me:

"Nothing is true, everything is permitted."

The C standard(s) are only defining sort of an order[3]ing on how this data
 types are related to each other:

```c_cpp
char < short < int < long < long long
```

And it means "a char is smaller than a short, which is smaller than an int,
 which is smaller than a long, which is smaller than a long long." :)

Enough for now! Change that `65` dude to some other values and see how your
 code will behave, and whenever you're done, a new blog post will be
 automagically created for you! (By the power of "When the pupil is ready to
 learn, a teacher will appear.")

Check this link to confuse yourself even more:
 <a href="https://en.wikipedia.org/wiki/C_data_types" target="_blank">
 https://en.wikipedia.org/wiki/C_data_types</a> (Yeah, go ahead!)

[1] Means "displaying on the screen" or shell or terminal window.

[2] Even if your favorite language has implemented them with blackjack and
 hookers(`std::string`), under the hood, they're still the same cool old ASCII
 digits. <a href="https://www.youtube.com/watch?v=5l3ipKcnYlQ" target="_blank">
 https://www.youtube.com/watch?v=5l3ipKcnYlQ</a>

[3] Out of the chaos.
