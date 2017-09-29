---
layout: post
title: "Variables"
category: c-language-tutorials
date: 2017-08-14 21:51:13 +0430
tags: [programming,unix,language,c,variable,value,terminal,decimal,short,int]
---

A variable is like a box in which you can keep something, and that "thing" is
 called, the **value**.

Imagine a program that prints a **char**(an alphabet letter) in several
 different ways:

```c_cpp
#include <stdio.h>

int main(int argc, char *argv[]){

  printf("The ASCII number for %c is %d.\n", 'A', 'A');

  printf("Soon you'll see how %c can be replaced with another letter!\n", 'A');

  return 0;
}
```

Personally I use variables only if:
 - I need to "recall" the same value more than twice **AND** the value may get
 changed.
 - Dynamic memory allocations. (Do **NOT** read about **malloc()**, it's not
 the time yet!)

For declaring(or defining or creating) a variable, we write its data type[1]
 followed by its name:

```c_cpp
#include <stdio.h>

int main(int argc, char *argv[]){

  int my_number;

  return 0;
}
```

**TIP**: It's a **good practice** to (read it: **YOU MUST**)set an initial
 value for your variables.[2] Try this example:

```c_cpp
#include <stdio.h>

int main(int argc, char *argv[]){

  int my_monster;
  int my_number = 0;

  printf("my_number is %d while my_monster is %d?!"
    "Run this program again to wonder more!\n", my_number, my_monster);

  return 0;
}
```

Oops! Welcome to the quantum world of C! probability and unpredictable-ity![3]

After all, variables are called **"variables"** because their value may
 **vary**:

```c_cpp
#include <stdio.h>

int main(int argc, char *argv[]){

  int my_number = 0;

  printf("my_number is just created and it holds %d inside.\n", my_number);

  my_number = 5;

  printf("Now it's %d.\n", my_number);

  my_number = 11;

  printf("And here it's %d.\n", my_number);

  return 0;
}
```

Same story for the **char**acters and you can declare them using the **char**
 keyword:

```c_cpp
#include <stdio.h>

int main(int argc, char *argv[]){

  char my_character = 'A';

  printf("my_character is just created and it holds %c inside.\n",
    my_character);

  printf("%c is the first letter in alphabet.\n", my_character);

  my_character = 'B';

  printf("my_character is now holding %c.\n", my_character);

  return 0;
}
```

### Rule #1: You can only use alphabet letters(both uppercase and lowercase)
 and underscores, but not hyphens.
### Rule #2: Variable names can **NOT** be started with numbers but they may
 have some digits in them. (wat?)

Also, when naming your variable, please consider the following "terms":
 - Make some sense.
 - Keep it short and meaningful.
 - Use plural form of the words whenever it's needed.
 - Follow the same naming convention. (lowercase_with_underscores, camelCase,
 PascalCase, etc.)

Example of a valid name which is just stupid:

```c_cpp
#include <stdio.h>

int main(int argc, char *argv[]){

  int my_number_9 = 127;

  printf("my_number_9 is %d. Such a revelation!\n", my_number_9);

  return 0;
}
```

While it's perfectly legal and allowed, it's a terrible idea and makes
 no sense. **DO NOT DO IT!**

Another **BAD EXAMPLE** of variable naming is using
 **long_long_stupid_names_which_makes_absolutely_no_sense**:

```c_cpp
#include <stdio.h>

int main(int argc, char *argv[]){

  int i_guess_i_will_use_this_number_somewhere = 15;

  printf("You see? Here I have my lovely %d!\n",
    i_guess_i_will_use_this_number_somewhere);

  return 0;
}
```

I guess it's enough of the theory and you gotta try some code on your own.
 Good luck!

Hint: It's always a good idea to have a look at how other people are doing it,
 and personally, I highly recommend the
 <a href="http://cvsweb.openbsd.org/cgi-bin/cvsweb/src/"
 target="_blank"> source code of the OpenBSD project</a> or nginx or redis.

[1] To tell the compiler **what sort of value we're going to store in it**.

[2] Simply because C does **NOT** "wipe" or "clean" the old value from your
 computer's memory upon the allocation.

[3] To be honest, I see it as a **feature**, since it does **NOT** do what I
 haven't asked for. Did I ever say "clear that area of RAM which had some
 values in it before" somewhere in my code? Of course not! :D
