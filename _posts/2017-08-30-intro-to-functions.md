---
layout: post
title: "Introduction to functions"
category: c-language-tutorials
date: 2017-08-30 15:10:37 +0430
tags: [programming,unix,language,ascii,char,array,string,pointer,function,void]
---

I'd like to describe the functions as:

 - Piece of code that is responsible for a certain task.
 - Helping you by keeping your codes organized and separated from each other.
 - Eliminate the need for writing the same code over and over again.

(And perhaps more, can't remember for now. stay tune for the updates!)

The very first function that you're going to create is called `say_hello`:

```c_cpp
#include <stdio.h>

void say_hello(){
  printf("Hello, world!\n");
}

int main(int argc, char *argv[]){

  say_hello();
  say_hello();
  say_hello();

  return 0;
}
```

Easy, isn't it?

The `void` keyword is used to declare that "this function does NOT return
 any values". No worries if you don't understand it, in the next post you'll
 see how we can actually `return` a value from a function.

A note by the ways: when defining functions, they should be "declared" prior
 to invoking(or calling) and if you don't respect this rule, you'll get an error
 similar to: (varies between compilers and environments)

```sh
my.c: In function ‘main’:
my.c:6:3: warning: implicit declaration of function ‘say_hello’ [-Wimplicit-function-declaration]
   say_hello();
```

Which is the compile error that you should get when trying to compile:

```c_cpp
#include <stdio.h>

int main(int argc, char *argv[]){

  say_hello();
  say_hello();
  say_hello();

  return 0;
}

void say_hello(){
  printf("Hello, world!\n");
}
```

So, how about an example which makes more sense?

```c_cpp
#include <stdio.h>

void say_hello(char *name){
  printf("Hello %s!\n", name);
}

int main(int argc, char *argv[]){

  say_hello("Alice");
  say_hello("Eve");
  say_hello("Bob");

  return 0;
}
```

That `char *name` dude is called **argument** and they're used when you want to
 send something "to" the variable. (In short, something from the "outside" will
 be available "inside" the variable.)

Enough already, make your own function that takes a number and display the
 halved so when you invoke(or call) `display_halve(24);` it will print `12`.

And by the ways, from now on, please compile your codes with the following
 options:

```sh
$ cc my.c -Wall -pedantic -std=c89
```

Good luck and be happy. 
